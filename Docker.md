#docker

Ubuntuコンテナを起動しBashで対話する
```terminal
$ docker container run -it --rm ubuntu bash
```

イメージ、コンテナ、ネットワーク、ボリュームを削除
```terminal
$ docker system prune --volumes
```

`compose.yaml` のあるディレクトリで Docker compose オブジェクトを削除
```terminal
$ docker compose down --rmi all --volumes --remove-orphans
```

