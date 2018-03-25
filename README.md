# KoalaAssistant
Kylo test application

## Postgres
Postgres container uses a datavolume in order to persist its data.

volume creation:
```bash
docker volume create kylo-data-pg
```

Launch Postgres container
```bash
docker run -d --rm --name kylo-pg --mount source=kylo-data-pg,target=/var/lib/postgresl/data -e POSTGRES_PASSWORD=$POSTGRES_PASSWORD -e POSTGRES_USER=$POSTGRES_USER -e POSTGRES_DB=$POSTGRES_DB postgres:9-alpine
```

Run postgres configuation script on the postgres container
```bash
docker run -it --rm --mount type=bind,source="$(pwd)"/configuration,target=/tmp  --link kylo-pg:pg postgres:9-alpine psql -h pg -U kylo -f /tmp/postgres_init.sql -v user_name=$POSTGRES_USER
```
