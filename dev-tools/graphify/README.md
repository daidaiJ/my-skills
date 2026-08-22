# Graphify

代码知识图谱工具，通过语义提取 + 社区检测构建持久知识图谱，用于架构级代码理解。

## 安装

```bash
uv tool install graphifyy
```

GitHub: https://github.com/safishamsi/graphify

## 使用场景

- **架构级理解** — 社区结构、跨文件关系、god nodes
- **语义语料** — 文档/论文/图片的语义提取（代码文件纯本地 AST，无 API 成本）
- **持久图谱** — `graphify-out/` 跨会话持久，`query/path/explain` 查询

## 与 codegraph 的分工

| | codegraph | graphify |
|---|---|---|
| 场景 | 符号级（定义/调用链/影响） | 架构级（社区/跨文件/语料） |
| 时机 | 编码任务中 | 会话早期理解架构 |

## 核心命令

| 命令 | 用途 |
|---|---|
| `graphify extract . --code-only` | 首次构建（纯本地 AST，无 API 成本） |
| `graphify update .` | 增量更新（只重提取变更文件） |
| `graphify query "..."` | 语义查询 |
| `graphify path A B` | 两符号间路径 |
| `graphify explain X` | 解释符号 |

## Qwen Code 集成：异步 hook 自动更新（推荐）

在 `~/.qwen/settings.json` 的 `SessionStart` 注册两个**异步** hook，会话开始时自动更新图谱（graphify 与 codegraph 各一个，互不阻塞）：

```json
{
  "hooks": {
    "SessionStart": [
      {
        "hooks": [
          {
            "type": "command",
            "command": "bash C:/Users/panda/.qwen/hooks/graphify-init.sh",
            "name": "graphify-init",
            "description": "Initialize or incrementally update Graphify index on session start",
            "async": true
          },
          {
            "type": "command",
            "command": "bash C:/Users/panda/.qwen/hooks/codegraph-init.sh",
            "name": "codegraph-init",
            "description": "Initialize or incrementally update CodeGraph index on session start",
            "async": true
          }
        ]
      }
    ]
  }
}
```

hook 脚本放在 `~/.qwen/hooks/`，从 stdin JSON 读取项目目录（`cwd`），带锁防并发：

**graphify-init.sh**（`graphify-out/` 存在则增量更新，否则首次构建）：

```bash
#!/usr/bin/env bash
# Graphify init/sync hook — runs async on Qwen Code session start.
set -e
HOOK_INPUT=$(cat)
PROJECT_DIR=$(echo "$HOOK_INPUT" | python3 -c "import sys,json; print(json.load(sys.stdin).get('cwd',''))" 2>/dev/null || echo "")
[ -z "$PROJECT_DIR" ] && PROJECT_DIR="$(pwd)"
cd "$PROJECT_DIR" 2>/dev/null || exit 0
GRAPHIFY="D:/Programs/graphify/bin/graphify.exe"   # 按本机安装位置调整
[ -x "$GRAPHIFY" ] || GRAPHIFY="graphify"
command -v "$GRAPHIFY" &>/dev/null || exit 0
LOCK=".graphify.lock"
[ -f "$LOCK" ] && exit 0
touch "$LOCK"
trap 'rm -f "$LOCK"' EXIT
if [ -d "graphify-out" ]; then
  "$GRAPHIFY" update . --no-cluster 2>/dev/null || true
else
  "$GRAPHIFY" extract . --code-only 2>/dev/null || true
fi
```

**codegraph-init.sh**（`.codegraph/` 存在则增量同步，否则初始化 + 索引）：

```bash
#!/usr/bin/env bash
# CodeGraph init/sync hook — runs async on Qwen Code session start.
set -e
HOOK_INPUT=$(cat)
PROJECT_DIR=$(echo "$HOOK_INPUT" | python3 -c "import sys,json; print(json.load(sys.stdin).get('cwd',''))" 2>/dev/null || echo "")
[ -z "$PROJECT_DIR" ] && PROJECT_DIR="$(pwd)"
cd "$PROJECT_DIR" 2>/dev/null || exit 0
command -v codegraph &>/dev/null || exit 0
[ -f ".codegraph/index.lock" ] && exit 0
if [ -d ".codegraph" ]; then
  codegraph sync --quiet 2>/dev/null || true
else
  codegraph init --index 2>/dev/null || true
fi
```

> 详细用法参见 [SKILL.md](./SKILL.md)