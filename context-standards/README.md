# 上下文规范

控制 Qwen Code 交互行为和上下文管理的 Skill。

| Skill | 用途 |
|-------|------|
| [caveman](./caveman/) | 压缩通信模式，减少 ~75% token 消耗 |
| [concise-verify](./concise-verify/) | 精要输出 + 验证兜底：先给最精简版本，细粒度标准逐条打分，低分即修（借鉴斯坦福 LLM-as-a-Verifier） |
| [i-have-adhd](./i-have-adhd/) | ADHD 友好输出：首行给下一步行动、多步工作编号、跨轮次重述状态、压制岔题、具体时间预估、让成果可见 |
| [show-me](./show-me/) | 最小可视化形态选择器：按话题强制选伪代码/调用树/组件树/文件树/Mermaid/diff 之一，跳过铺垫直接上图 |
| [handoff](./handoff/) | 会话交接，生成交接文档并保存到 `.qwen/handoff/`，新会话可直接恢复 |
| [stop-slop](./stop-slop/) | 移除 AI 写作模式，让文本更自然（支持中英文） |
| [improve-agent-md](./improve-agent-md/) | 手动触发的指令文件优化：用 `<important if>` 条件块重写 AGENTS.md/CLAUDE.md/SKILL.md，对抗"相关性过滤"导致的指令被无视，配套裁剪原则（来源：humanlayer/skills improve-claude-md，MIT） |
