## How to create dump

### Go inside any running postgres docker

#### Run either of two from / (cd /)

```
pg_dump -U postgres  --no-acl  --no-owner  postgres > /raw_dump_acl.sql
pg_dump -U postgres postgres > /raw_dump.sql
```

## Overall Process

### Dockerfile: copy the dump.sql(or any other name) to /docker-entrypoint-initdb.d/ as all the sql scripts will be automatically run during container startup

```
FROM postgres:9.6.6-alpine 
COPY *.sql /docker-entrypoint-initdb.d/
RUN chmod a+r /docker-entrypoint-initdb.d/*
```

### Create docker image
```
docker build -t "$IMAGE_NAME:$NEW_TAG" . 
docker login -u "$DOCKER_USER" -p "$DOCKER_PASS" 
docker push "$IMAGE_NAME:$NEW_TAG"
```



## More Help

```
I've done something like what is described in this article in the past, by dumping my real db and then use an initialization script to load the dumped sql and populate the container's db:

https://medium.com/@sherryhsu/set-up-postgresql-database-using-with-production-data-using-docker-f164694341f1

Init script is discussed further down the page in Postgres docs:

https://hub.docker.com/_/postgres/
```


