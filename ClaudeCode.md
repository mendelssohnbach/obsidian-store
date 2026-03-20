# AI

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

