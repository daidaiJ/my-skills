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
```
