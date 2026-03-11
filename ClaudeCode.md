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