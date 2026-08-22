# CodeGraph

代码知识图谱工具，通过预索引的符号关系和调用图，大幅减少工具调用次数和 token 消耗。

## 安装

```bash
npm i -g @colbymchenry/codegraph
```

GitHub: https://github.com/colbymchenry/codegraph

## 使用场景

- **搜索符号定义** — 精确定位函数、类、类型、接口等的定义位置
- **追踪调用链** — 查找某个符号的上下游调用关系
- **变更影响分析** — 修改公共接口前，评估波及范围
- **任务级上下文** — 编码任务开始前，一次调用获取入口点、相关符号和代码片段
- **项目结构概览** — 快速了解项目的模块划分

## 前置条件

```bash
codegraph init --index <project_path>
```

## 核心命令

| 命令 | 用途 | 替代方案 |
|---|---|---|
| `codegraph context "任务描述"` | 任务级上下文 | Explore 子代理 |
| `codegraph query <符号名>` | 搜索符号定义 | `grep_search` |
| `codegraph callers <符号名>` | 查找调用方 | 手动 grep + read_file |
| `codegraph callees <符号名>` | 查找被调用方 | 手动 grep + read_file |
| `codegraph impact <符号名>` | 变更影响分析 | 试错 |
| `codegraph files` | 项目文件结构 | 多层 `list_directory` |
| `codegraph sync` | 增量同步索引 | 通常自动同步 |

## 典型工作流

```
1. codegraph context "修改 /api/users 端点增加分页功能"
2. codegraph query "GetUsers" --kind function
3. codegraph callers GetUsers
4. codegraph callees GetUsers
5. codegraph impact GetUsers --depth 2
```

## Qwen Code 集成：异步 hook 自动更新（推荐）

在 `~/.qwen/settings.json` 的 `SessionStart` 注册两个**异步** hook，会话开始时自动更新图谱（codegraph 与 graphify 各一个，互不阻塞）：

```json
{
  "hooks": {
    "SessionStart": [
      {
        "hooks": [
          {
            "type": "command",
            "command": "bash C:/Users/panda/.qwen/hooks/codegraph-init.sh",
            "name": "codegraph-init",
            "description": "Initialize or incrementally update CodeGraph index on session start",
            "async": true
          },
          {
            "type": "command",
            "command": "bash C:/Users/panda/.qwen/hooks/graphify-init.sh",
            "name": "graphify-init",
            "description": "Initialize or incrementally update Graphify index on session start",
            "async": true
          }
        ]
      }
    ]
  }
}
```

hook 脚本放在 `~/.qwen/hooks/`，从 stdin JSON 读取项目目录（`cwd`），带锁防并发：

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

> 详细用法参见 [SKILL.md](./SKILL.md)
