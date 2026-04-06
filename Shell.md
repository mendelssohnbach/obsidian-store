#Linux

コマンド履歴を完全消去
```terminalo
$ history -c && history -w
```

**Bash** 厳格モード
```bash
#!/usr/bin/env bash
set -euo pipefail
IFS=$'\n\t'
```

