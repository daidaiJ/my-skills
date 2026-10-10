# 开发工具

提升编码效率和代码质量的工具类 Skill。

| Skill | 用途 |
|-------|------|
| [codegraph](./codegraph/) | 代码知识图谱，五大能力：任务上下文/符号搜索/双向调用链/变更影响/受影响测试选择（affected），一次调用替代多轮 grep/read_file |
| [cbm](./cbm/) | codebase-memory-mcp fork 架构级图谱查询（低频重型）：架构概览/复杂度热点排行/commit 影响半径，与 codegraph 分工互补；CLI 全量 17 工具或 MCP 最小 4 工具面（同一份预索引图谱）；需安装 fork CLI（[release](https://github.com/daidaiJ/codebase-memory-mcp/releases) 提供 Windows amd64 二进制） |
| [graphify](./graphify/) | 代码知识图谱，架构级理解/社区结构/跨文件关系，含 Qwen Code 异步 hook 自动更新 |
| [ast-grep](./ast-grep/) | AST 级结构化搜索与批量重构：精确匹配调用点/函数声明、排除注释与字符串误报；实测记录 Go 选择器模式解析坑与 YAML 结构规则绕过 |
| [mermaid](./mermaid/) | mmdx 图表渲染导出：20 种 mermaid 图（含 kanban/radar/treemap）+ 表格/列表/卡片 → SVG+PNG，官方变量体系主题 + 中文字体 + ELK 布局，批量并发、--json/--profile agent 友好（[发布产物](https://github.com/daidaiJ/mmdx/releases)） |
| [code-review](./code-review/) | 双轴评审：Standards（极严格可维护性审查：code judo、1000 行红线、Fowler smells）+ Spec（忠实实现来源规格） |
| [improve-codebase-architecture](./improve-codebase-architecture/) | 架构改进扫描：找「浅模块→深模块」的 deepening 机会，产出可视化 HTML 报告（before/after 图），选定候选后进入 grill-me 决策树；依赖同目录 codebase-design 与 domain-modeling（来源：mattpocock/skills，MIT） |
| [codebase-design](./codebase-design/) | 深模块设计词汇表与原则（module/interface/depth/seam/adapter/leverage/locality、删除测试），设计或重构模块接口时使用（来源：mattpocock/skills，MIT） |
| [domain-modeling](./domain-modeling/) | 领域建模与上下文沉淀：维护 CONTEXT.md 词汇表与 docs/adr/ 决策记录，架构对话中即时落盘（来源：mattpocock/skills，MIT） |
| [use-modern-go](./use-modern-go/) | 现代 Go 编码规范（JetBrains 官方）：写/改 Go 代码前按 go.mod 版本拉取适用规范，避免生成过时写法；内置 Windows 二进制免下载（来源：JetBrains/go-modern-guidelines，Apache-2.0） |
| [defect-detective](./defect-detective/) | 缺陷侦探：设计+实现+工程三轴深度审查，产出带 file:line 证据的 P0/P1/P2 分级缺陷清单 |
| [diagnosing-bugs](./diagnosing-bugs/) | 疑难 bug 诊断：先建红绿反馈循环 → 最小化复现 → 假设 → 插桩 → 修复 + 回归测试 → 复盘 |
| [trace-to-plan](./trace-to-plan/) | 反向 wayfinder：.issue 线索链多轮重入调查，多边信号交叉收敛 → ROI 决策 → 业务对齐方案 → bench 闭环 |
| [github](./github/) | GitHub 平台操作：gh CLI 管理 issues / PR / CI |
| [self-verify](./self-verify/) | 自验证循环：派子智能体审计工作，PASS/FAIL 裁决，失败自动重试；含 ABC 闭卷知识验证回路与堆栈追踪调试（Go/JS/Python/Rust） |
| [excalidraw-diagram](./excalidraw-diagram/) | Excalidraw 图解生成：流程/架构/协议图，本地 Playwright 渲染 PNG 预览校验 |
| [mcp-builder](./mcp-builder/) | MCP 服务器开发指南：Python (FastMCP) / TypeScript (MCP SDK)，含评估体系 |
| [playwright-browser-automation](./playwright-browser-automation/) | 直接调用 Playwright API 的浏览器自动化：导航、交互、抓取、截图、PDF、录屏 |
| [mcp-registry-publish](./mcp-registry-publish/) | 发布 MCP server 到官方 MCP Registry：-registry 后缀 tag 显式触发、.mcpb 打包（[mcpb-tool-cli](https://github.com/daidaiJ/mcpb-tool-cli) 开源 CLI，go install 获取）、server.json 生成、OIDC 免密钥发布与验证闭环 |
| [verify-this](./verify-this/) | 可证伪验证主张：复述为可证伪形式 → baseline/treatment 同条件对比原始产物 → 三态裁决 VERIFIED / NOT VERIFIED / INCONCLUSIVE（来源：cursor/plugins，MIT） |
| [tdd](./tdd/) | Bug 修复先写失败测试再修：失败在前、最小修复在后，含「何时不该写测试」的清醒边界（来源：cursor/plugins，MIT） |
| [thermo-nuclear-review](./thermo-nuclear-review/) | 分支级安全与正确性审计：bug / 破坏性变更 / DevEx 回归（secrets、env、端口、脚本）/ feature-flag 泄漏，与 defect-detective（全仓三轴）互补（来源：cursor/plugins，MIT） |
| [blast-radius](./blast-radius/) | 上线前破坏半径分析：找「唯一安全事实」并用真实代码证明（5 级置信阶梯），前瞻视角与 defect-detective 互补（来源：cursor/plugins，MIT） |
| [control-cli](./control-cli/) | 本地 PTY/tmux harness 驱动交互式 CLI：确定性复现 bug、键盘流验证、启动/内存 profiling、终端录屏（Windows 走 PTY/WSL）（来源：cursor/plugins，MIT） |
| [control-ui](./control-ui/) | 本地 Playwright/CDP harness 驱动 Web/Electron UI：截图、无障碍快照、CPU profile / 堆快照取证（来源：cursor/plugins，MIT） |
| [cli-for-agents](./cli-for-agents/) | 面向 coding agent 的 CLI 设计/评审规范：非交互优先、分层 --help 带示例、stdin/管道、幂等、dry-run、机器可读成功输出（来源：cursor/plugins，MIT） |
| [model-params](./model-params/) | 模型参数与价格速查：curl + jq 查 OpenRouter 与 models.dev 两个公开目录，确认上下文/tool call/structured output/reasoning 档位与每 1M token 价格，支持按实时汇率折算人民币（四个国内外免 key 汇率源）；免安装免 key（[modelq](https://github.com/daidaiJ/modelq) 配套单 skill） |
| [principle-type-system-discipline](./principle-type-system-discipline/) | 工程原则卡：非法状态不可表示、brand 语义原语、外部数据边界解析、穷尽变体、从权威 schema 派生 |
| [principle-prove-it-works](./principle-prove-it-works/) | 工程原则卡：用真实产物验证（跑功能/读实际值/查 diff），不信代理指标与自我汇报 |
| [principle-laziness-protocol](./principle-laziness-protocol/) | 工程原则卡：偏向删除与最小变更，平坦调用层级，合并决策点，堵小泄漏 |
| [principle-encode-lessons-in-structure](./principle-encode-lessons-in-structure/) | 工程原则卡：重复指令编码为 lint/脚本/运行时检查等机制，而非更多文字 |
| [principle-foundational-thinking](./principle-foundational-thinking/) | 工程原则卡：先定数据结构再写逻辑，脚手架先行，并发共享先隔离 |
| [principle-sequence-verifiable-units](./principle-sequence-verifiable-units/) | 工程原则卡：拆成各自可验证的小单元串行推进，提交顺序即论证 |
| [principle-never-block-on-the-human](./principle-never-block-on-the-human/) | 工程原则卡：可逆工作不阻塞等人，事后纠偏；确认只留给不可逆操作 |
| [principle-boundary-discipline](./principle-boundary-discipline/) | 工程原则卡：校验与错误处理集中在系统边界，内部纯函数信任类型 |

> principle-* 8 张卡来源：cursor/plugins pstack（MIT），条件触发式原则卡，正文纯提示词零依赖。

show-me（最小可视化形态选择器）归入[上下文规范](../context-standards/)，不在本分类。
