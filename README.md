# My Skills

Qwen Code 自定义 Skill 集合，按用途分类组织。

## 目录

### [开发工具](./dev-tools/) — 提升编码效率和代码质量

| Skill | 用途 |
|-------|------|
| [codegraph](./dev-tools/codegraph/) | 代码知识图谱，符号搜索/调用链追踪/变更影响分析 |
| [mermaid](./dev-tools/mermaid/) | Mermaid 图表渲染，支持 SVG 和 ASCII 输出 |

### [媒体处理](./media-tool/) — 音视频和图片处理

| Skill | 用途 |
|-------|------|
| [ffmpeg](./media-tool/ffmpeg/) | 视频/音频处理：合并、裁剪、转码、提取帧/音频、GIF、字幕 |
| [imagemagick](./media-tool/imagemagick/) | 图片处理：调整大小、裁剪、格式转换、水印、合成、批处理 |

### [办公工具](./office-tool/) — 文档处理全家桶

| Skill | 用途 |
|-------|------|
| [docx](./office-tool/docx/) | Word 文档创建、编辑、模板填写（.docx/.dotx） |
| [markdown-to-epub](./office-tool/markdown-to-epub/) | Markdown 转 EPUB 电子书，支持 Kindle |
| [pdf](./office-tool/pdf/) | PDF 读取、合并、拆分、表单填写、OCR、图片插入、表格创建 |
| [pptx](./office-tool/pptx/) | PowerPoint 演示文稿，含 193 个预置模板和 QA 工具链 |
| [xlsx](./office-tool/xlsx/) | 电子表格处理，支持公式、图表、复杂表格填写 |
| [liteparse](./office-tool/liteparse/) | 轻量 PDF 文本提取，本地处理无依赖 |

### [规划与设计](./planning/) — 需求分析和方案设计

| Skill | 用途 |
|-------|------|
| [designer](./planning/designer/) | 多轮对话式项目规划，输出完整计划文档 |
| [grill-me](./planning/grill-me/) | 方案压力测试，逐条审视设计决策 |

### [上下文规范](./context-standards/) — 交互行为和上下文管理

| Skill | 用途 |
|-------|------|
| [caveman](./context-standards/caveman/) | 压缩通信模式，减少 ~75% token 消耗 |
| [handoff](./context-standards/handoff/) | 会话交接，生成可被新 agent 继续的文档 |
| [stop-slop](./context-standards/stop-slop/) | 移除 AI 写作模式，让文本更自然（支持中英文） |

### [通用工具](./common/) — Skill 开发和管理

| Skill | 用途 |
|-------|------|
| [dir-organizer](./common/dir-organizer/) | 整理和优化项目目录结构 |
| [skill-creator](./common/skill-creator/) | 创建、编辑、优化 Skill，运行性能测试 |
| [teach](./common/teach/) | 在工作区内教授用户新技能或概念 |

### [学术科研](./science/) — 科研全流程辅助

| Skill | 用途 |
|-------|------|
| [citation-management](./science/citation-management/) | 学术引用管理：搜索论文、提取元数据、验证引用、生成 BibTeX |
| [experimental-design](./science/experimental-design/) | 实验设计：随机化、区组、因子、交叉等方案规划 |
| [exploratory-data-analysis](./science/exploratory-data-analysis/) | 探索性数据分析：200+ 数据格式自动检测与综合 EDA |
| [hypothesis-generation](./science/hypothesis-generation/) | 假说生成：从观察/数据出发构建可检验假说和验证实验 |
| [paper-lookup](./science/paper-lookup/) | 论文检索：跨 10 个学术 API 搜索论文、预印本和开放获取全文 |
| [peer-review](./science/peer-review/) | 同行评审：基于清单的结构化评审，涵盖方法学和报告标准 |
| [scholar-evaluation](./science/scholar-evaluation/) | 学术评估：多维度定量评分与可操作反馈 |
| [scientific-brainstorming](./science/scientific-brainstorming/) | 科研头脑风暴：跨学科创意探索与研究空白识别 |
| [scientific-critical-thinking](./science/scientific-critical-thinking/) | 科学批判性思维：评估证据质量，应用 GRADE 等分级框架 |
| [scientific-schematics](./science/scientific-schematics/) | 科学示意图：AI 生成出版级科学图表 |
| [scientific-visualization](./science/scientific-visualization/) | 科学可视化：面向 Nature/Science/Cell 的出版级图表 |
| [statistical-analysis](./science/statistical-analysis/) | 统计分析：全流程引导式统计分析与 APA 格式报告 |
| [statistical-power](./science/statistical-power/) | 统计功效与样本量：研究规划的样本量和功效计算 |

### [分析工具](./analyzer/) — Skill 质量和安全分析

| Skill | 用途 |
|-------|------|
| [skill-quality-analyzer](./analyzer/skill-quality-analyzer/) | Skill 质量分析：五维度评估（结构/安全/UX/代码/集成），支持综合报告、交互审查、认证三种模式 |
| [skill-security-analyzer](./analyzer/skill-security-analyzer/) | Skill 安全扫描：检测 40+ 恶意模式（命令注入、YAML 注入、数据泄露、时间炸弹、typosquatting 等） |

## 安装

将 Skill 目录复制到 `~/.qwen/skills/` 下即可使用。

```bash
# 示例：安装 codegraph skill
cp -r dev-tools/codegraph ~/.qwen/skills/codegraph
```

### 外部依赖

部分 Skill 需要额外安装：

```bash
# codegraph
npm i -g @colbymchenry/codegraph

# ffmpeg（视频/音频处理）
# Windows: scoop install ffmpeg  或  choco install ffmpeg
# macOS:   brew install ffmpeg
# Linux:   sudo apt install ffmpeg

# imagemagick（图片处理）
# Windows: scoop install imagemagick  或  choco install imagemagick
# macOS:   brew install imagemagick
# Linux:   sudo apt install imagemagick

# skill-security-analyzer（安全扫描）
# 需要 Python 3.8+，依赖已内置（PyYAML）
python3 --version

# --- 学术科研系列 ---

# 统计分析 + 统计功效（共享核心依赖）
uv pip install "pingouin>=0.6" "scipy>=1.11" "statsmodels>=0.14.6" "numpy>=1.26" pandas matplotlib seaborn
uv pip install "pymc>=5.0" "arviz>=1.0"   # 贝叶斯统计
uv pip install lifelines                   # 生存分析

# 实验设计
uv pip install "numpy>=1.26" "pandas>=2.0" pyDOE3

# 引用管理
uv pip install requests bibtexparser biopython crossref-commons pylatexenc
uv pip install scholarly                   # Google Scholar（可选）
uv pip install selenium                    # Scholar 稳定抓取（可选）

# 科学可视化
uv pip install matplotlib seaborn plotly

# 探索性数据分析（按数据格式按需安装）
uv pip install biopython                   # 生物信息学格式

# 科学示意图
pip install requests                       # AI 生成示意图

# 假说生成（LaTeX 报告）
# 需要 XeLaTeX 或 LuaLaTeX（TeX Live / MiKTeX）
# Windows: scoop install texlive  或  choco install miktex
# macOS:   brew install --cask mactex
# Linux:   sudo apt install texlive-full
tlmgr install tcolorbox xcolor fontspec fancyhdr titlesec enumitem booktabs natbib
```

#### 学术科研环境变量（可选）

以下 API Key 均为可选，未配置时 skill 仍可工作（降级或提示获取方式）：

| 环境变量 | 用途 | 获取地址 |
|----------|------|----------|
| `OPENROUTER_API_KEY` | 科学示意图、引用管理、假说生成等的 AI 增强功能 | https://openrouter.ai/keys |
| `NCBI_API_KEY` | PubMed 检索加速（3→10 req/s） | https://www.ncbi.nlm.nih.gov/account/settings/ |
| `NCBI_EMAIL` | NCBI Entrez 请求标识 | — |
| `S2_API_KEY` | Semantic Scholar 检索加速 | https://www.semanticscholar.org/product/api#api-key-form |
| `CORE_API_KEY` | CORE 全文获取 | https://core.ac.uk/services/api |
| `OPENALEX_API_KEY` | OpenAlex 检索加速 | https://openalex.org/settings/api |
