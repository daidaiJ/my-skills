# 上下文规范

控制 Qwen Code 交互行为和上下文管理的 Skill。

| Skill | 用途 |
|-------|------|
| [caveman](./caveman/) | 压缩通信模式，减少 ~75% token 消耗 |
| [concise-verify](./concise-verify/) | 精要输出 + 验证兜底：先给最精简版本，细粒度标准逐条打分，低分即修（借鉴斯坦福 LLM-as-a-Verifier） |
| [handoff](./handoff/) | 会话交接，生成交接文档并保存到 `.qwen/handoff/`，新会话可直接恢复 |
| [stop-slop](./stop-slop/) | 移除 AI 写作模式，让文本更自然（支持中英文） |
