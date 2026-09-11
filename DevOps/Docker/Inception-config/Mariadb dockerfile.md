```dockerfile
FROM debian:bookworm

RUN apt-get update && apt-get upgrade && apt install -y mariadb-server

COPY entrypoint.sh /entrypoint.sh

RUN chmod +x /entrypoint.sh

EXPOSE 3306

ENTRYPOINT ["/entrypoint.sh"]

CMD ["mysqld", "--user=mysql", "--bind-address=0.0.0.0"]
```
EXPOSE 3306 is to open his port at this specifically

`mysqld --user=mysql --bind-address=0.0.0.0

Is the command that start mariadb after it up.
The --user flag  i mandatory to access the db and the --bind is to accept connection from every incoming IP adress.

