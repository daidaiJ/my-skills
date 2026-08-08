# 论文写作流水线（融合自 OpenSquilla meta-paper-write / paper-* 系列）

## 论文写作流水线（融合自 OpenSquilla meta-paper-write / paper-* 系列）

来源：`meta-paper-write` 编排器 + `paper-source-curator` / `paper-outline-author` /
`paper-citation-planner` / `paper-section-author` / `paper-revision-author` /
`paper-abstract-author`（origin: opensquilla-original，许可证 Apache-2.0）。
本 skill 的检索能力是这条流水线的第一步——先用上面的文献 API 找到资料并整理出
BibTeX，再按下面的顺序产出论文。每步输出是下一步的输入，遵循各自固定的输出契约。

### 流水线顺序

1. **来源整理（paper-source-curator）**：把检索结果 + BibTeX 整理为 source pack。
   选 20–40 个可用引用并标注 `refN` 键；区分 PRIMARY_SOURCES /
   SUPPORTING_SOURCES / EXCLUDED_OR_WEAK_SOURCES；优先官方文档、论文、项目仓库、
   标准、发布说明；不发明来源与键。
2. **提纲（paper-outline-author）**：写五段式提纲 ABSTRACT / INTRODUCTION /
   METHOD / RESULTS / DISCUSSION，规划 6,500–8,000 词；每段要有具体内容
   （子主题、方法选择、预期结果），非摘要各节合计分配 ≥20 个不同引用键。
3. **引用规划（paper-citation-planner）**：把论文论点映射到 BibTeX 键，输出
   CITATION_PLAN：按 INTRODUCTION / METHOD / RESULTS / DISCUSSION 分区，
   每条 claim 配 `cite` + `role`（background / prior work / gap / method /
   comparison / limitation…）；引用只分配给论点，不分配给填充句。
4. **分节写作（paper-section-author）**：按写作计划逐节写 LaTeX 片段
   （abstract / introduction / related_work / method / results / experiments /
   discussion / conclusion）。固定开篇环境（`\section{...}`），`target_words`
   为下限（非摘要节 90%–125%），只用 `cite_keys_hint` 里的键，不编造数据，
   不输出注释。
5. **整稿修订（paper-revision-author）**：把各节片段合成为连贯 LaTeX 正文
   `\section{Introduction}` → `\section{Discussion}`；保留图表块与标签、
   保持 ≥20 个有效引用键、统一术语/贡献/指标/基线、删除重复段落；
   不含摘要、文献表。
6. **摘要（paper-abstract-author）**：最后写 250–350 词 `\begin{abstract}`，
   只总结已修订正文的论点与证据，不引入新 claim，默认不带引用。

### 硬性规则

- 不编造引用与实验结果：引用键必须来自 source pack / bibliography。
- 全文长度与引用预算以用户请求或 writing plan 为准，不套固定页数。
- 每一环节输出有固定契约（Plain text 或纯 LaTeX 片段），便于下游直接衔接。
- 普通论文请求走紧凑起草路径；仅当用户明确要求完整稿件 / PDF / 长文时，
  才走完整流水线 + LaTeX 编译。
