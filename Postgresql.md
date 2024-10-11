#db 

```terminal
$ docker container run --name db --detach --env POSTGRES_PASSWORD=secret --publish 5432:5432 postgres
$ psql --host=127.0.0.1 --port=5432 --username=postgres
...
Password for user postgres: secret
...
postgres=# 
```

```terminal
$ docker run --name my-postgres --env POSTGRES_PASSWORD=mypassword --detach postgres
$ docker exec -it my-postgres psql -h localhost -U postgres -d postgres
```

