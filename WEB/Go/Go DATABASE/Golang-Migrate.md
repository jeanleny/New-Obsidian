
`golang-migrate` is a small CLI program and a go library whose job is to manage [[database Migrations]]

#### 1. Installation
```bash
go install -tags 'postgres' github.com/golang-migrate/migrate/v4/cmd/migrate@latest
```
- the `-tags 'postgres'` 
	Is to specify what database. golang-migrate support a lot of database and by default will create a lot of dependencies we dont need.
  So the **tag** flag only takes which driver we  need.

#### 2. Generating migration

```bash
migrate create -ext sql -dir migrations -seq migration_name
```
This does not modify the DB, it only creates empty files.
- the `-ext sql` is for the extension to use
- the `-dir migrations` where to put them
- `-seq` is to use sequential integers (00001, 00002) instead of the default Unix timestamp

#### 3. Apply to the db
```bash
migrate -database "postgres://clicker:clicker@localhost:5432/clicker?sslmode=disable" \
	        -path migrations up
```
To apply it, you need
- connection string, what we call the [[DSN]] (data source name) via the tag `-database`.
- the `-path` is to find the .sql files
- `up` is a subcommand which tells golang migrate to take the newer than the current migration.



