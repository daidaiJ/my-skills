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

> 详细用法参见 [SKILL.md](./SKILL.md)
