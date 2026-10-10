# Handoff — 跨会话任务交接

将当前会话的工作进度固化为下一个会话可以自动关联的 handoff 记录，通过 `AGENTS.md` 的入口摘要块实现跨会话无缝接续。

## 使用

```
/handoff
/handoff 继续优化数据库查询性能
```

带参数时，参数描述下次会话的重点方向，handoff 文档会据此调整内容。

## 存储

```
项目根目录/AGENTS.md            入口摘要块（≤10 行/块，恢复场景读到这里通常就够）
项目根目录/.handoff/<任务名>.md  热层详情卡（覆盖写；完成 → archive/ 冷层）
```

`.handoff/` 默认写入 `.gitignore`（交接噪音与本地现场不进仓库历史）；用户明确要求跨设备同步时，按 `references/writing.md`「git 同步开关」节摘除 ignore，交接记录随仓库走。

## 核心文件

| 文件 | 说明 |
|------|------|
| [`SKILL.md`](SKILL.md) | 瘦核心：双场景路由、核心原则、双层结构速览（两场景细节全在 references，按需加载） |
| [`references/writing.md`](references/writing.md) | 写交接场景全套：存储结构、git 同步开关、12 节模板、AGENTS.md 摘要块标准、膨胀与腐化防线（摘要块 + 详情层/关联文档两道）、写入流程与自检、完成清理 |
| [`references/recovery.md`](references/recovery.md) | 恢复交接场景：轻路径——通常 AGENTS.md 摘要即可接续，下钻顺序与回写衔接 |
| [`references/progress-formats.md`](references/progress-formats.md) | 可选：三种进度格式（Todo / 检查清单 / 量化描述） |
| [`references/verification.md`](references/verification.md) | 可选：验证核验清单 + 未验证事项填写规则 |
