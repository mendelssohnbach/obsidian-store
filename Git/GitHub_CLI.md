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
$ gh pr create --assignee @me --title "New feature" --body "Description of new feature"
```

プルリクエストを作成、`body` はブラウザで記述
```terminal
$ gh pr create --assignee @me --title 'Happy' --web
```

プルリクエスト一覧
```terminal
$ gh pr list
```

プルリクエストをマージ
```terminal
$ gh pr merage PR_NUMBER
```

イシューを作成
```terminal
$ gh issue create --title "Bug report" --body "Description of the bug"
```

未解決イシュー一覧
```
$ gh issue list
```

ワークフロー一覧
```terminal
$ gh workflow list
```

ワークフローをトリガー
```terminal
$ gh workflow run WORKFLOW_NAME
```
