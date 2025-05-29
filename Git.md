#Git

空ディレクトリをチェックイン
```Terminal
$ mkdir logs/
$ touch logs/.gitkeep
```

`.gitignore` 追加
```text
# Keep empty logs/ directory.
/logs/*
!/logs/.gitkeep
```