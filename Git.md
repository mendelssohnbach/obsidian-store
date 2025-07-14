#Git

## データ構造に対してどのような操作をしているかというのをイメージするよう意識すること

リポジトリに「圧縮ファイル」「ツリー」「コミット」ファイルを作成することでデータを保存する

1. ワークツリーというのが作業場
	1. ワークツリーでファイルを変更
2. ステージというのはコミットする変更を準備する場所
	1. 変更をステージに追加
	2. ファイルの中身をまず圧縮して、次にインデックスのファイル名にマッピング情報を記載する
3. リポジトリというのがスナップショットを記録する場所
	1. リポジトリをスナップショットとして記録
	2. インデックスのファイルの内容を元に、「ツリー1」というファイル構成を表したファイルを作成
4. ステージとインデックスは同義語

## git config
**git** 専用のエイリアスは `git config` で登録する
- `git config --global alias.ALIAS_COMMAND GIT_COMMAND`
	- システム全体に登録
- `git config alias.ALIAS_COMMAND GIT_COMMAND`
	- システム全体に登録
```
$ git config --global alias.ci commit
```

## 空ディレクトリをチェックイン
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

## git restore
- `git restore FILE_NAME`: ファイルを、最後にコミットされた状態に戻す
- `git restore --staged .`: ステージされたすべてを取り消す
	- エイリアスとして登録済み: **git unstag**
- `git restore --source=COMMIT_HASH OR FINE_NAME`: 特定のコミットの状態にファイルを戻す
## git diff
- `git diff`: インデックスとワーキングツリーの差分
- `git diff --staged`: インデックスとHEADの差分
- `git diff --cached`:  インデックスとHEADの差分

## git fetch/pull
- `git fetch orign`: リモートから取得のみ
- `git pull': `fetch` + `merge
	- 現在のブランチにマージされる(ブランチ名は無視)`

## git rm
- `git rm FILE_NAME`: ファイルを削除
- `git rm --cached FILE_NAME`: 履歴管理から削除するが、ワークツリーには残す
```
$ git rm index.html
/最新のコミットから指定のファイルをステージエリアに戻す
$ git reset HEAD FILE_NAME
// 指定のファイルをステージエリアからワーキングツリーに戻す
$ git checkout FILE_NAME
// 指定のファイルをローカルリポジトリから削除
$ git rm --cached index.html
```

## git checkout
**ワーキングツリー** のファイルに対して行う
- `git checkout -- FILE_NAME`: `FILE_NAME` ファイルの変更を取り消す
- `git checkout -- DIR_NAME`: `DIR_NAME` ディレクトリの変更を取り消す
- `git checkout -- .`: 全ファイルの変更を取り消す

# git merge
- Fast Forward: git merge New_Branch
ブランチが枝分かれしていないき、元々のブランチからNewブランチを作成し、取り込む
- Auto Merge: git merge Aother_Branch
複数のブランチで変更コミットがあり、他方のブランチを取り込む。新しいコミットがいるがつくられる

## git branch
- `git branch -d BRANCH_NAME`: 指定したブランチを削除
- `git branc -D BRANCH_NAME`: 未マージのファイルがあっても指定したブランチを削除

## GitHub Flow
1. mainブランチからtopicブランチを作成
2. featureブランチにてファイルを変更し、コミット
3. featureブランチと同名でGitHubへプッシュ
4. プッシュできたらプルリクエストを送信
5. プルリクエストを受け取ったら、コードレビュー
6. コードレビュー監査後、mainブランチにマージ
7. featureブランチを削除
8. mainブランチを本番サーバにデプロイ

## git rebase
`git rebase BRANCH_NAME`: 他のブランチへの変更分を現在のブランチに取り込む
- `git config --globale pull.rebase ture`: `pull` の挙動を `rebase` に置き換える
	- 置き換えにより `pull` した歴史が残らない
```
[pull]
	rebase = true
```

### rebase コミットの文言修正
- `git rebase -i COMMIT_ID`: 指定した `COMMIT_ID` のコミットをやり直す
	- コミットエディタが起動したら、修正するコミットの `pick を `edit` に修正する
	- ファイルを修正ごステージングし、 `git commit --amend` を実行
### rebase コミットの順番入れ替え
- コミットを並び替えるには、コミットエディタで対象のコミット順番を入れ替える
### rebase コミットをまとめる
- コミットをまとめるには、コミットエディタで対象のコミットを `squash` に変更する
	- `squash` に成功すると再度コミットエディタが起動するので保存し終了

## git tag
コミットを参照しやすくするために、わかりやすい名前付けをおこなうこと
- `git tag`: tag 一覧を表示
- `git tag -a TAG_NAME -m "MESSAGE"`: 注釈付きタグきを作成
- `git tag -a TAG_NAME COMMIT_ID -m "MESSAGE"`: 過去のコミットidに注釈付きタグを作成
- `git show TAG_NAME`: タグの詳細を表示
- `git push REMOTE_NAME TAG_NAME`: 単一のタグをリモートリポジトリに送信
- `git push origin --tags`: タグを一斉に送信

## git stash
- `git stash`: 作業を一時避難する
- `git stash list`: 避難した作業を確認
- `git stash apply`: 避難した作業を復元
- `git stash drop`: 最新の避難した作業を削除
- `git stash clear `: 全部の避難した作業を削除