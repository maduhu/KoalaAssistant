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

## Elastic Search

Elestic search container creation.
```bash
docker run -d -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" --name kylo-es docker.elastic.co/elasticsearch/elasticsearch:6.6.8
```

## ActiveMQ

ActiveMQ volume creation
```bash
docker volume create kylo-data-mq
```

ActiveMQ container creation
```bash
docker run -d --rm --name kylo-mq -e ACTIVEMQ_ADMIN_LOGIN=$MQ_ADMIN_USER -e ACTIVEMQ_ADMIN_PASSWORD=$MQ_ADMIN_PASSWORD -p 8161:8161 -p 61616:61616 -p 61613:61613 --mount source=kylo-data-mq,target=/data webcenter/activemq:5.14.3
```
