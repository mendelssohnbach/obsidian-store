# AI

## スラッシュコマンド

```terminal
/modle # 現在のモデルを確認
/modle opus # Opusに切り替え
/modle sonnet # Sonnetに切り替え
/model opusplan # 複雑な推論をopusで行う
/usage # プラン使用量の確認
/init # プロジェクトに `CALUDE.md` を作成
/ide # VSCode連携機能ON
/rewind # チャット履歴の巻き戻し
/exit # Claudeを終了
/logout # ユーザーアカウントからログアウト
/permission # パーミッションを追加/編集
/btw # 副題質問を差し込む
/insights # 過去１ヶ月の分析レポート出力
/simplify # コードレビュー
/export # 会話内容をMarkdownに出力
/init # プロジェクトの構造/使用技術/コーディング規約/ClaudeCodeが知っておくべき情報を記載
/context # コンテキストウィンドウの可視化
/clear # コンテキストをリセット
/compact # コンテキストを要約圧縮
/bashes # バックグラウンド実行コマンドを呼び出す
/add-dir # 他ディレクトリを含める
/reviw #N # N版のプルリクをレビューする
/agetns # サブエージェント作成
/hooks # hooksを対話モードで作成
/security-review # セキュリティ分析
/privacy-settings # プライバシー設定画面呼び出し
/sandbox # サンドボックス環境
/mcp # mcpサーバー一覧表示
/terminal-setup # Shift+Enterによる改行を有効にする
```

## MCPを安全に使う

`settings.json` 編集
```
// ~/.claude/settings.json に以下を追加
{
  "enableAllProjectMcpServers": false,
  "permissions": {
    "disableBypassPermissionsMode": "disable"
  }
}
```

**Claude Code** をリセット
```
$ claude code
> reset
```

`proved_tools.json` が存在しないか確認
```
$ ls -la ~/.claude/
```

## Claude Cowork

```terminal
# GPGキーを追加
$ curl -fsSL https://aaddrick.github.io/claude-desktop-debian/KEY.gpg \
  | sudo gpg --dearmor -o /usr/share/keyrings/claude-desktop.gpg
# リポジトリを追加
$ echo "deb [signed-by=/usr/share/keyrings/claude-desktop.gpg arch=amd64,arm64] \
  https://aaddrick.github.io/claude-desktop-debian stable main" \
  | sudo tee /etc/apt/sources.list.d/claude-desktop.list
# インストール
$ sudo apt update
$ sudo apt install claude-desktop
# 依存パッケージを確認
$ laude-desktop --doctor
# KVMバックエンドを使う
$ sudo apt install qemu-system-x86 qemu-utils socat
# アプリメニューから `Claude` を起動
```

