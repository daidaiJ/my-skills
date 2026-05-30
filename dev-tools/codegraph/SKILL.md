---
name: codegraph
description: 当需要搜索符号定义、追踪调用链、分析变更影响、理解陌生模块时，用预索引的代码知识图谱一次调用替代多轮 grep/glob/read_file，工具调用减少 60%+、token 消耗降低 50%+
---

# CodeGraph — 代码知识图谱辅助

## 核心原则

CodeGraph 预索引了项目的符号关系和调用图，一次 CLI 调用即可替代多轮 grep/glob/read_file 操作。当项目根目录存在 `.codegraph` 文件夹时，**优先使用 codegraph 命令**获取代码上下文，显著减少工具调用次数和 token 消耗。

## 前置条件

项目已初始化 codegraph（`.codegraph` 目录存在）。如不存在，先运行：
```bash
codegraph init --index <project_path>
```

## 工作流：6 个核心命令

### 1. `context` — 任务级智能上下文（首选）

开始任何编码任务前，先用 `context` 获取整体上下文，一次调用返回入口点、相关符号和代码片段。

```bash
# 为一个任务描述构建上下文，返回相关符号和代码
codegraph context "实现用户登录的 JWT 认证" --max-nodes 20

# 返回 Markdown 格式，包含文件路径、符号名称、源码片段
codegraph context "优化数据库查询性能" --format markdown --max-nodes 15
```

**何时使用：** 接到任务后、动手写代码前的第一步。替代 Explore 子代理的多轮文件扫描。

### 2. `query` — 按名称搜索符号

精确定位函数、类、类型、接口等符号定义。

```bash
# 搜索名为 HandleLogin 的符号
codegraph query HandleLogin

# 限定符号类型（function, class, method, type, interface, variable）
codegraph query "User" --kind class --limit 10

# JSON 输出，便于解析
codegraph query "ParseToken" --json
```

**何时使用：** 需要找到某个函数/类/类型的定义位置时，替代 `grep "func HandleLogin"`。

### 3. `callers` — 谁调用了这个符号

查找所有调用指定函数/方法的上游代码。框架感知：查询 controller 的 callers 会暴露关联的 URL 路由。

```bash
# 查找谁调用了 HandleLogin
codegraph callers HandleLogin --limit 20

# JSON 输出
codegraph callers "UserService.Create" --json
```

**何时使用：** 修改函数签名前，先了解调用方；理解请求链路时追踪入口到处理函数。

### 4. `callees` — 这个符号调用了什么

向下追踪函数的调用链，了解它依赖了哪些下游逻辑。

```bash
# 查看 HandleLogin 内部调用了哪些函数
codegraph callees HandleLogin

# 限制返回数量
codegraph callees "ProcessOrder" --limit 15
```

**何时使用：** 理解一个复杂函数的内部流程；评估修改某函数是否会影响其下游。

### 5. `impact` — 变更影响分析

修改代码前，用 `impact` 评估波及范围。遍历 callers 和 callees，给出完整的影响半径。

```bash
# 分析修改 UserRepo.Find 的影响范围
codegraph impact "UserRepo.Find" --depth 3

# JSON 输出
codegraph impact "Config.Load" --depth 2 --json
```

**何时使用：** 重构前评估风险；修改公共接口前确认影响范围。

### 6. `files` — 文件结构概览

快速查看项目的索引文件结构，比遍历文件系统更快。

```bash
# 查看项目文件结构
codegraph files

# 按扩展名过滤
codegraph files --filter "*.go"

# 限制目录深度
codegraph files --max-depth 2

# JSON 输出
codegraph files --json
```

**何时使用：** 需要快速了解项目模块划分时，替代 `list_directory` 的多层遍历。

### 补充：`sync` — 增量同步索引

当 codegraph context/query 返回的结果看起来不完整或过时时，手动触发增量同步：

```bash
codegraph sync [path]
```

> 通常 codegraph 会自动监听文件变更并同步（防抖 2s），一般不需要手动执行。

## 典型工作流示例

### 场景：修改一个 API 端点的处理函数

```
第一步：获取任务上下文
  codegraph context "修改 /api/users 端点增加分页功能"

第二步：定位目标符号
  codegraph query "GetUsers" --kind function

第三步：了解谁在调用（确认路由绑定）
  codegraph callers GetUsers

第四步：了解内部调用链（确认数据层依赖）
  codegraph callees GetUsers

第五步：评估变更影响
  codegraph impact GetUsers --depth 2

→ 此时已有足够信息开始编写代码，无需额外的 grep/read_file
```

### 场景：理解一个不熟悉的模块

```
第一步：整体上下文
  codegraph context "理解 auth 模块的认证流程"

第二步：浏览文件结构
  codegraph files --filter "*.go" --max-depth 3

第三步：追踪核心符号的调用链
  codegraph callers AuthService.Validate
  codegraph callees AuthService.Validate
```

## 与现有工具的优先级

| 场景 | 优先使用 | 而非 |
|---|---|---|
| 开始编码任务前 | `codegraph context` | Explore 子代理 |
| 查找函数/类定义 | `codegraph query` | `grep_search` |
| 追踪调用关系 | `codegraph callers/callees` | 手动 grep + read_file |
| 评估变更风险 | `codegraph impact` | 猜测 + 试错 |
| 查看项目结构 | `codegraph files` | 多层 `list_directory` |

**注意：** 当 codegraph 返回不足时（如搜索非符号内容、查看具体实现逻辑），仍使用 `read_file` 读取完整源码。codegraph 提供的是符号级视图，不是源码全文。
