# n8n-docker
A simple and starter docker template for N8N Application + Postgres + NGINX example file.


# n8n with PostgreSQL

Starts n8n with PostgreSQL as database.


## Start

To start n8n with PostgreSQL simply start docker-compose by executing the following
command in the current folder.


**IMPORTANT:** Before you do that change the default users and passwords are in the [`.env`](.env) file!

```
docker-compose up -d
```

To stop it execute:

```
docker-compose stop
```

## Configuration

The default name of the database, user and password for PostgreSQL can be changed in the [`.env`](.env) file in the current directory.
