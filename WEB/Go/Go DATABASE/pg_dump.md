To create a whole DB schema, you can use `pg_dump`

### 1 In a container 
Use the docker exec cmd to create the schema and set it in a file that will be created on your local machine.
```bash
docker compose exec db_container_name \
    pg_dump --schema-only -U postgresUsername db_name > schema.sql
```
