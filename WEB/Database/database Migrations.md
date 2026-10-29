A database **migration** is the modification of a database.
It's most of the time a SQL file containing the last modifications.
It does not contains the whole db schema, just the sequences of changes.


Imagine, you have this Database .sql file :
```SQL
CREATE TABLE user (
	id SERIAL PRIMARY KEY,
	login VARCHAR NOT NULL,
	money BIGINT NOT NULL DEFAULT 0
);
```

But somethings missing, you want to add an email row.
You will have a new **migration**, a new version control of your database.

### Remind
You dont edit the current migration, you create another one with you're Database framework. This way you're data are kept.

In order 

#### Create migration 

This cmd will create the sql file in the migration dir with a given file name "add_password_to_users"
```bash
migrate create -ext sql -dir migrations -seq add_password_to_users
```

#### Add the SQL content to the file to both created file

The up.sql : Used to add a DB modification:
```sql
ALTER TABLE users ADD COLUMN password VARCHAR NOT NULL DEFAULT '';
```

The down.sql  : Used to revert a DB modification
```sql
ALTER TABLE users DROP COLUMN password;
```

#### Apply migration 
This will apply the migration to the database
``` bash
migrate -path migrations -database "postgres://user:pass@localhost:5432/scheduler?sslmode=disable" up
```
