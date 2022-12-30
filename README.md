# hydenv-backend
Docker-compose script for hydenv application

This repository includes a `docker-compose.yaml` to spin off the `hydenv` CLI along with a
PostgreSQL container with PostGIS extension installed. You need to add two more environment
files, before the application can be used.
A `postgis.env` is needed to set the `postgres` super-user password like:

```env
POSTGRES_PASSWORD=yourSecretPassword
```

It is important to keep the `.env` file private and choose a complicated password, as the default
config of this application exposes the 5432 port for PostgreSQL to the public.

Secondly, the hydenv CLI needs the connection to the database. 

```bash
docker-compose run --rm hydenv database install -i
```

Either mount the `/root` path and use the usual install as described in [hydenv-database](github.com/data-hydenv/hydenv-database). This will create a connection file, which is mounted into the container.

The maybe safer way is to create the second `hydenv.env` here and populate it with the connection, so that the 
password is only set as environment variable:

```env
POSTGRES_HOST=postgres
POSTGRES_PORT=5432
POSTGRES_USER=hydenv
POSTGRES_PASSWORD=thePasswordChosenDuringInstall
POSTGRES_DBNAME=hydenv
```

If you chose different connection details during the install step, you need to change the `hydenv.env` file
accordingly.
