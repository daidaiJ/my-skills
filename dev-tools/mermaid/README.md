# Mermaid

mmdx 图表渲染导出：把 ```mermaid / ```table / ```list / ```card 围栏块渲染成高质量 SVG/PNG 图片。

- 20 种 mermaid 图型（含 kanban / radar / treemap 等 v11 全量）+ 表格/列表/卡片
- 官方变量体系主题（非 CSS 脏修），内置中文字体（Noto Sans SC）与 ELK 布局
- 批量并发渲染、`--json` / `--profile`，为 agent 工作流设计
- 单文件二进制，免 Node 环境

## 获取（按优先级）

1. **Release 二进制**（推荐）：https://github.com/daidaiJ/mmdx/releases
   ```bash
   curl -L -o "$TMP/mmdx.exe" https://github.com/daidaiJ/mmdx/releases/latest/download/mmdx-windows-x64.exe
   ```
   （GitHub CDN 超时时加代理前缀 `HTTPS_PROXY=http://127.0.0.1:7897`）
2. 本机已构建：`D:\CODE\ai\mmdx\dist\mmdx-windows-x64.exe`
3. 源码动态运行（需 bun）：仓库 `D:\CODE\ai\mmdx`，`bun run src/cli.ts`

## 快速开始

```bash
# 默认：同目录 <name>-m1.svg/.png 每块一文件
mmdx diagram.md

# 定向输出 PNG / SVG
mmdx diagram.md -f png -o out

# stdin + JSON 结果
echo "graph LR; A[自检] --> B{通过}" | mmdx - -f png -o "$TMP/check" --json --quiet
```

渲染后按 SKILL.md §1d 做像素级自检（`--json` 拿尺寸/墨水占比，异常查 §2 错误速诊表）。

## 文件结构

- `SKILL.md` — 完整用法：选型对照表、写图规则、渐进渲染档位、错误速诊、主题定制（内置主题 / `--css` 片段 / `--theme-js` 换色）、常见坑
- 仓库与详细文档：https://github.com/daidaiJ/mmdx

> 本目录只保留 SKILL.md；安装与运行细节见 SKILL.md「CLI 获取」与「环境自检」。
