# 规划与设计

项目启动前的需求分析和方案设计类 Skill。

| Skill | 用途 |
|-------|------|
| [designer](./designer/) | 多轮对话式项目规划，输出完整计划文档 |
| [grill-me](./grill-me/) | 方案压力测试 + 内联文档维护：拷问设计决策，术语解析即写入 CONTEXT.md，满足条件提议 ADR |
| [sdd-brainstorm](./sdd-brainstorm/) | 轻量需求头脑风暴 — 先查代码库再讨论 |
| [sdd-spec](./sdd-spec/) | 将讨论结论转化为结构化规格文档 + 任务拆解 |
| [sdd-implement](./sdd-implement/) | 按 Ticket 逐个实现，复用优先，内置进度追踪 |
| [tech-outline-planner](./tech-outline-planner/) | 技术文章/系统设计大纲规划：C-I-S-T 叙事框架 + "Given before New" 原则，输出架构评审级大纲 |

## SDD 套件设计哲学

**默认最轻路径，按需阶梯升级。**

三个 skill 都遵循 L0/L1/L2 三级设计：

| 级别 | 原则 | 典型操作 |
|------|------|---------|
| **L0**（默认） | 纯对话 + 文件读写，零额外工具调用 | grep 扫代码、对话讨论、写 markdown |
| **L1**（按需） | 单个平台能力介入 | LSP 查接口、worktree 隔离变更 |
| **L2**（复杂） | 子智能体/子会话委派 | 架构师建模、审查员 review |

**升级判断标准**：不用会出问题才用，不是能用就用。

```
/sdd-brainstorm → /sdd-spec → /sdd-implement
     需求讨论         规格文档        逐票实现
     (L0 默认)       (L0 默认)      (L0+todo)
```

阶段间可插入 `/grill-me` 压力测试（兼维护领域模型文档）或 `/handoff` 保存上下文。
