# Handoff — 跨会话任务交接

将当前会话的工作进度固化为下一个会话可以自动关联的 handoff 记录，通过 `AGENTS.md` 的入口摘要块实现跨会话无缝接续。

## 使用

```
/handoff
/handoff 继续优化数据库查询性能
```

带参数时，参数描述下次会话的重点方向，handoff 文档会据此调整内容。

---

## 渐进式阅读

根据你的需要，按需深入不同深度的文档，无需全部读完。

| 阶段 | 读什么 | 时长 |
|------|--------|------|
| **快速上手** | `SKILL.md`（前 80 行：目标、原则、存储结构、双层结构） | ~3 分钟 |
| **开始写 handoff** | `SKILL.md` 完整版 + [进度格式参考](references/progress-formats.md) | ~10 分钟 |
| **执行任务 / 调试** | `SKILL.md` 完整版 + 所有 references | ~15 分钟 |

---

## 快速导航

### 核心文档

| 文件 | 内容 |
|------|------|
| [`SKILL.md`](SKILL.md) | 完整 skill 指南：存储结构、双层结构、AGENTS.md 摘要块、写入 / 恢复 / 清理三个执行流程 |
| [`references/progress-formats.md`](references/progress-formats.md) | 三种进度格式（Todo 列表 / 检查清单 / 量化描述）的选择指南和模板 |
| [`references/verification.md`](references/verification.md) | 写入前 / 写入后 / 恢复时 / 清理时的逐条核验清单 |

---

## 核心概念

### 项目隔离

handoff 只属于单个项目，始终存放在项目根目录下的 `.handoff/` 子目录。禁止写入任何全局路径或仓库外路径。

### 双层结构

- **详情层**：`.handoff/<任务名>.md`，完整版，12 个必填节
- **入口摘要层**：`AGENTS.md` 中的精简引用块，最少一句话关联 handoff

两层互相引用，详情层按需全文读取，摘要层让 Agent 一眼看到全局。

### 渐进式批量

不需要时不必读完所有内容。写简单任务只看 SKILL.md；有测试结果要量化时再读 `progress-formats.md`；完成前要逐条核验时再读 `verification.md`。
