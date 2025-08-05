#docker

デーモンの状態確認
```
$ sudo systemctl status docker 
```

Ubuntuコンテナを起動しBashで対話する
```terminal
$ docker run -d -it --name ubuntu-sample ubuntu
$ docker exec -it ubuntu-sample bin/bash
```

イメージ、コンテナ、ネットワーク、ボリュームを削除
```terminal
$ docker system prune --volumes
```

`compose.yaml` のあるディレクトリで Docker compose オブジェクトを削除
```terminal
$ docker compose down --rmi all --volumes --remove-orphans
```

