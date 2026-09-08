Postgres is a free and open-source object-relational database management system (ORDMBS), which means that it has realtional capabalities and an object-oriented design using SQL.

Here is a example of docker-compose to launch the db :

```yml
services:
  db:
    image: postgres:17
    container_name: clicker-db
    restart: unless-stopped

    environment:
      POSTGRES_USER: user
      POSTGRES_PASSWORD: pass
      POSTGRES_DB: clicker

    ports:
      - "5432:5432"

    volumes:
      - postgres_data:/var/lib/postgresql/data

volumes : 
  postgres_data:

```
Then use `docker compose up -d` to launch it in the background

