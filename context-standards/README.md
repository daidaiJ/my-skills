# 上下文规范

控制 Agent 交互行为和上下文管理的 Skill。

| Skill | 用途 |
|-------|------|
| [caveman](./caveman/) | 压缩通信模式，减少 ~75% token 消耗 |
| [concise-verify](./concise-verify/) | 精要输出 + 验证兜底：先给最精简版本，细粒度标准逐条打分，低分即修（借鉴斯坦福 LLM-as-a-Verifier） |
| [i-have-adhd](./i-have-adhd/) | ADHD 友好输出：首行给下一步行动、多步工作编号、跨轮次重述状态、压制岔题、具体时间预估、让成果可见 |
| [show-me](./show-me/) | 最小可视化形态选择器：按话题强制选伪代码/调用树/组件树/文件树/Mermaid/diff 之一，跳过铺垫直接上图（来源：humanlayer/skills 的 show-me，MIT） |
| [handoff](./handoff/) | 会话交接：把进度固化为 `.handoff/` 双层记录（详情卡 + `AGENTS.md` ≤10 行摘要块），新会话自动接续；`.handoff/` 默认 gitignore，按需开启 git 同步即可跨设备接力 |
| [stop-slop](./stop-slop/) | 移除 AI 写作模式，让文本更自然（支持中英文）；含 unslop 扩展目录（references/unslop-rules.md，稳定编号规则，来源：cursor/plugins，MIT） |
| [show-me-your-work](./show-me-your-work/) | 长任务/无人值守运行的决策日志：TSV 一行一决策（决策/理由/证据指针/结果），追加式可审计，含日志-转录核对与跨模型审查回路（来源：cursor/plugins，MIT） |
| [improve-agent-md](./improve-agent-md/) | 手动触发的指令文件优化：用 `<important if>` 条件块重写 AGENTS.md/CLAUDE.md/SKILL.md，对抗"相关性过滤"导致的指令被无视，配套四条精简原则（来源：humanlayer/skills 的 improve-claude-md，MIT） |
