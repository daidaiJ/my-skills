# 开发工具

提升编码效率和代码质量的工具类 Skill。

| Skill | 用途 |
|-------|------|
| [codegraph](./codegraph/) | 代码知识图谱，五大能力：任务上下文/符号搜索/双向调用链/变更影响/受影响测试选择（affected），一次调用替代多轮 grep/read_file |
| [graphify](./graphify/) | 代码知识图谱，架构级理解/社区结构/跨文件关系，含 Qwen Code 异步 hook 自动更新 |
| [ast-grep](./ast-grep/) | AST 级结构化搜索与批量重构：精确匹配调用点/函数声明、排除注释与字符串误报；实测记录 Go 选择器模式解析坑与 YAML 结构规则绕过 |
| [cbm](./cbm/) | codebase-memory-mcp fork 架构级图谱查询（低频重型）：架构概览/复杂度热点排行/commit 影响半径，与 codegraph 分工互补；需安装 fork CLI（[release](https://github.com/daidaiJ/codebase-memory-mcp/releases) 提供 Windows amd64 二进制） |
| [mermaid](./mermaid/) | mmdx 图表渲染导出：20 种 mermaid 图（含 kanban/radar/treemap）+ 表格/列表/卡片 → SVG+PNG，官方变量体系主题 + 中文字体 + ELK 布局，批量并发、--json/--profile agent 友好（[发布产物](https://github.com/daidaiJ/mmdx/releases)） |
| [show-me](./show-me/) | 讲解话题时强制选最小可视化形态（伪代码/调用树/组件树/文件树/Mermaid/diff），跳过铺垫直接上图（来源：humanlayer/skills，MIT） |
| [code-review](./code-review/) | 双轴评审：Standards（极严格可维护性审查：code judo、1000 行红线、Fowler smells）+ Spec（忠实实现来源规格） |
| [improve-codebase-architecture](./improve-codebase-architecture/) | 架构改进扫描：找「浅模块→深模块」的 deepening 机会，产出可视化 HTML 报告（before/after 图），选定候选后进入 grill-me 决策树；依赖同目录 codebase-design 与 domain-modeling（来源：mattpocock/skills，MIT） |
| [codebase-design](./codebase-design/) | 深模块设计词汇表与原则（module/interface/depth/seam/adapter/leverage/locality、删除测试），设计或重构模块接口时使用（来源：mattpocock/skills，MIT） |
| [domain-modeling](./domain-modeling/) | 领域建模与上下文沉淀：维护 CONTEXT.md 词汇表与 docs/adr/ 决策记录，架构对话中即时落盘（来源：mattpocock/skills，MIT） |
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
