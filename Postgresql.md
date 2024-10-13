#db 

`compose.yaml`
```
# ./compose.yaml
services:
  db:
    image: postgres:16
    ports:
      - '5432:5432'
    restart: always
    environment:
      POSTGRES_USER: user
      POSTGRES_PASSWORD: password
      POSTGRES_DB: sample
    volumes:
      - db-data:/var/lib/postgresql/data

  pgadmin:
    image: dpage/pgadmin4
    ports:
      - 8080:80
    volumes:
      - pgadmin-data:/var/lib/pgadmin
      - ./config/servers.json:/pgadmin4/servers.json
    environment:
      PGADMIN_DEFAULT_EMAIL: user@example.com
      PGADMIN_DEFAULT_PASSWORD: password
      PGADMIN_CONFIG_SERVER_MODE: 'False'
      PGADMIN_CONFIG_MASTER_PASSWORD_REQUIRED: 'False'
    depends_on:
      - db

volumes:
  db-data:
  pgadmin-data:
```

`server.json`
```
// ./config/server.json
{
  "Servers": {
    "1": {
      "Name": "db",
      "Group": "Servers",
      "Host": "db",
      "Port": 5432,
      "MaintenanceDB": "postgres",
      "Username": "user",
      "SSLMode": "prefer"
    }
  }
}
```

起動と停止
```
// 起動
$ docker compose up
// 停止
$ docker compose down
```

ログインできるのか確認せよ
```
$ docker compose exec -it db bash
// psql -h "ホスト名" -U "ユーザー名" -p "ポート番号" -d "DB名"
$ psql -h localhost -U postgres -p 5432 -d sample
```



