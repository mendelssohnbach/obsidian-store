#Git

アカウントの確認
```terminal
$ gh auth status
```

新規リポジトリをプライベートモードかつ `README.md` 付きで作成
```terminal
$ gh repo create demo-repo --private --add-readme -c
```

プルリクエスト一覧(対象プロジェクト内で)
```terminal
$ gh pr list
```

リポジトリを規定のブラウザで開く(対象プロジェクト内で)
```terminal
$ gh browse
```

プルリクエストを作成
```terminal
$ gh pr create --assignee @me --title 'Happy' --body 'Happy Text'
```

プルリクエストを作成、`body` はブラウザで記述
```terminal
$ gh pr create --assignee @me --title 'Happy' --web
```

プルリクエストをマージ
```terminal
$ gh pr merage 123
```

ワークフロー一覧
```terminal
$ gh workflow list
```
