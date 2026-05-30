# Mermaid

Mermaid 图表渲染工具，支持 SVG 图形输出和 ASCII 终端输出。

## 依赖

使用 `beautiful-mermaid` 库，首次运行时自动安装。

## 支持的图表类型

| 类型 | 语法 | 适用场景 |
|------|------|----------|
| Flowchart | `graph TD/LR` | 流程、决策 |
| Sequence | `sequenceDiagram` | API 调用、交互 |
| State | `stateDiagram-v2` | 状态机 |
| Class | `classDiagram` | OOP 设计 |
| ER | `erDiagram` | 数据库 Schema |

## 快速开始

### SVG 输出（默认）

```bash
npx tsx scripts/render.ts diagram.mmd --output diagram.svg
echo "graph LR; A-->B-->C" | npx tsx scripts/render.ts --stdin --output flow.svg
```

### ASCII 输出（终端）

```bash
npx tsx scripts/render.ts diagram.mmd --ascii
echo "graph TD; Start-->End" | npx tsx scripts/render.ts --stdin --ascii
```

输出示例：
```
┌───────┐     ┌─────┐
│ Start │────▶│ End │
└───────┘     └─────┘
```

### 主题（仅 SVG）

```bash
npx tsx scripts/render.ts diagram.mmd --theme github-dark --output out.svg
```

使用无效主题名查看可用列表（如 `--theme ?`）

## 文件结构

- `scripts/render.ts` — 渲染脚本
- `references/syntax.md` — Mermaid 语法速查

> 详细用法参见 [SKILL.md](./SKILL.md)
