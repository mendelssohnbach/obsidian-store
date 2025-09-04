#tools 

CREATE(POST)

```terminal
$ curl -X POST \
     -H "Content-Type: application/json" \
     -d '{
       "title": "新しいポスト",
       "content": "これは新しい投稿です",
       "author": "John Doe"
     }' \
     https://api.example.com/posts
```

READ(GET)

```terminal
# 単一リソースの取得
$ curl https://api.example.com/posts/123

# リソース一覧の取得
$ curl https://api.example.com/posts?page=1&limit=10
```

UPDATE(PUT/PATCH)

```terminal
$ curl -X PUT \
     -H "Content-Type: application/json" \
     -d '{
       "title": "更新されたタイトル",
       "content": "更新された内容",
       "author": "John Doe"
     }' \
     https://api.example.com/posts/123

# PATCHによる部分更新
$ curl -X PATCH \
     -H "Content-Type: application/json" \
     -d '{
       "title": "更新されたタイトル"
     }' \
     https://api.example.com/posts/123
```

DELETE

```terminal
$ curl -X DELETE https://api.example.com/posts/123
```

ファイルアップロード

```terminal
# 単一ファイル
$ curl -F "file=@localfile.jpg" https://api.example.com/upload

# 複数ファイル
$ curl -F "file1=@file1.jpg" -F "file2=@file2.jpg" https://api.example.com/upload

# メタデータ付きアップロード
curl -F "file=@localfile.jpg" \
     -F "description=My vacation photo" \
     https://api.example.com/upload
```

