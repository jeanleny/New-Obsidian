A database **migration** is version of a database.
It's most of the time a SQL file containing the database table and organisation.

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
