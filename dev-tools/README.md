# 开发工具

提升编码效率和代码质量的工具类 Skill。

| Skill | 用途 |
|-------|------|
| [codegraph](./codegraph/) | 代码知识图谱，一次调用替代多轮 grep/read_file |
| [mermaid](./mermaid/) | Mermaid 图表渲染，支持 SVG 和 ASCII 输出 |
| [code-review](./code-review/) | 双轴评审：Standards（极严格可维护性审查：code judo、1000 行红线、Fowler smells）+ Spec（忠实实现来源规格） |
| [use-modern-go](./use-modern-go/) | 现代 Go 编码规范（JetBrains 官方）：写/改 Go 代码前按 go.mod 版本拉取适用规范，避免生成过时写法；内置 Windows 二进制免下载（来源：JetBrains/go-modern-guidelines，Apache-2.0） |
| [defect-detective](./defect-detective/) | 缺陷侦探：设计+实现+工程三轴深度审查，产出带 file:line 证据的 P0/P1/P2 分级缺陷清单 |
| [diagnosing-bugs](./diagnosing-bugs/) | 疑难 bug 诊断：先建红绿反馈循环 → 最小化复现 → 假设 → 插桩 → 修复 + 回归测试 → 复盘 |
| [trace-to-plan](./trace-to-plan/) | 反向 wayfinder：.issue 线索链多轮重入调查，多边信号交叉收敛 → ROI 决策 → 业务对齐方案 → bench 闭环 |
| [github](./github/) | GitHub 平台操作：gh CLI 管理 issues / PR / CI |
| [self-verify](./self-verify/) | 自验证循环：派子智能体审计工作，PASS/FAIL 裁决，失败自动重试 |
| [excalidraw-diagram](./excalidraw-diagram/) | Excalidraw 图解生成：流程/架构/协议图，本地 Playwright 渲染 PNG 预览校验 |
| [mcp-builder](./mcp-builder/) | MCP 服务器开发指南：Python (FastMCP) / TypeScript (MCP SDK)，含评估体系 |
| [playwright-browser-automation](./playwright-browser-automation/) | 直接调用 Playwright API 的浏览器自动化：导航、交互、抓取、截图、PDF、录屏 |
| [mcp-registry-publish](./mcp-registry-publish/) | 发布 MCP server 到官方 MCP Registry：-registry 后缀 tag 显式触发、.mcpb 打包（[mcpb-tool-cli](https://github.com/daidaiJ/mcpb-tool-cli) 开源 CLI，go install 获取）、server.json 生成、OIDC 免密钥发布与验证闭环 |
