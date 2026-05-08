```sh
#!/bin/bash
set -e

mkdir -p /run/mysqld
chown -R mysql:mysql /run/mysqld

echo "mariadb start"

if [ ! -d "/var/lib/mysql/$MYSQL_DATABASE" ]; then
	mysqld --user=mysql --skip-networking &
	MYSQL_PID=$!
	until mysqladmin ping --socket=/run/mysqld/mysqld.sock --silent 2>/dev/null; do
	    echo "mariadb waiting"
	    sleep 1
	done

	echo "init db"
	mysql --socket=/run/mysqld/mysqld.sock << EOF
	CREATE DATABASE IF NOT EXISTS $MYSQL_DATABASE;
	CREATE USER IF NOT EXISTS '$MYSQL_USER'@'%' IDENTIFIED BY '$MYSQL_PASSWORD';
	GRANT ALL PRIVILEGES ON $MYSQL_DATABASE.* TO '$MYSQL_USER'@'%';
	ALTER USER 'root'@'localhost' IDENTIFIED BY '$MYSQL_ROOT_PASSWORD';
	FLUSH PRIVILEGES;
EOF

	echo "db created"

	kill $MYSQL_PID
	wait $MYSQL_PID 2>/dev/null || true
fi
	echo "start mariadb"
	exec "$@"
```

**Resume**
This script will launch mariadb in the background the loop (no networking just socket)
It is necessary because mariadb is a CLIENT that needs a running server to connect to.
You can't run SQL without a server already listening.
Then we can kill its process once the db is created by keeping its PID.

``set -e
Stops the scripts immediately if any cmd fails

``mkdir -p /run/mysqld
create the directory where MariaDB puts its socket file
-p means: no error if it already exists, create parent dirs too 
This directory doesn't exist by default in debian:bookworm

chown gives ownership of the entire directory to the mysql:user.
This is because mariadb runs as the mysql user and needs write access to create the socket file

the if condition is here to check if the database already exists yet(if the docker env is down but didnt delete the volumes)
This path is created by Mariadb when it runs the SQL `CREATE DATABASE`

`mysqld --user=mysql --skip-networking &` is the basic cmd to launch mariadb --skip networking is to avoid opening ports at this stage and & flag is to run mariadb in the background.

`until mysqladmin ping --socket=/run/mysqld/mysqld.sock --silent 2>/dev/null; do
`
This will loop until mysqladmin ping succeeds.
The ping tests the connection with mariadb to see if the DB is ready.
--socket connect via socket file instead of TCP (because --skip-networking is on)

`mysql --socket=/run/mysqld/mysqld.sock << EOF`
This what launches the db.
Everything is stored in a heredoc to write the complete db setup.

```SQL
  CREATE DATABASE IF NOT EXISTS $MYSQL_DATABASE;
        # create the wordpress database
        # IF NOT EXISTS → no error if it already exists
        # $MYSQL_DATABASE → "wordpress" from your .env

        CREATE USER IF NOT EXISTS '$MYSQL_USER'@'%' IDENTIFIED BY '$MYSQL_PASSWORD';
	    # create the wordpress user
        # '$MYSQL_USER'@'%' → username from .env, % means "from any host/IP"
        # % is critical because WordPress is in a DIFFERENT container with its own IP
        # IDENTIFIED BY → sets the password from .env

        GRANT ALL PRIVILEGES ON $MYSQL_DATABASE.* TO '$MYSQL_USER'@'%';
        # give the wordpress user full access to the wordpress database
        # $MYSQL_DATABASE.* → all tables inside the wordpress database
        # without this the user exists but can't read or write anything

        ALTER USER 'root'@'localhost' IDENTIFIED BY '$MYSQL_ROOT_PASSWORD';
        # set a password for the root account
        # 'root'@'localhost' → root can only connect from inside this container
        # $MYSQL_ROOT_PASSWORD comes from your .env

        FLUSH PRIVILEGES;
        # force MariaDB to reload its permission tables immediately
        # without this the changes above might not take effect right away
```

`exec "$@"` is what stops the bash script here.
Its actually an expand to all arguments passed to the script.
In this case ./entrypoint.sh takes the CMD present in the docker file. 
```dockerfile
# exec mysqld --user=mysql --bind address=0.0.0.0
CMD : mysqld --user=mysql --bind address=0.0.0.0
```
