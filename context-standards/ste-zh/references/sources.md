# 来源、映射与局限

抓取日期：2026-10-25。标注「已核验」的条目来自原文或标准正文；标注「未核验」的只有二手摘要。

## 一、为什么做这个

2026 年 8 月，Matt Pocock（[@mattpocockuk](https://x.com/mattpocockuk)）在全局 CLAUDE.md 里加了一条：

> Always talk in ASD-STE100 Simplified Technical English.

这条推文是 [status/2084753070437609606](https://x.com/mattpocockuk/status/2084753070437609606)。次日他补了一条，说被动式指令效果有限，改为发布 `/wait-what` skill，用 STE 定基调（[status/2084941367659168064](https://x.com/mattpocockuk/status/2084941367659168064)）。**这两条只看到搜索摘要，没有打开原帖，未核验。**

同期 Andrej Karpathy 也提过让模型用 ASD-STE100 解释东西（见 searchenginejournal、towardsai 的报道，以及 STC README 引用的推文链接；**二手来源，未核验**）。这一轮讨论催生了一批 STE 类 skill：英文的 `/plain`、`wait-what`，中文的 STC。

这些 skill 都用英文规则。中文的歧义来源和英文不同，直接照搬会漏掉主要失分点：名词化结构、长定语、「以上」的端点、「可以」的许可与能力、省略主语、开放列举。本 skill 补这一块，并定义与 `i-have-adhd`、`caveman` 的组合方式。

## 二、ASD-STE100 事实（已核验）

- 全称 ASD-STE100 Simplified Technical English，受控自然语言，用于技术文档。
- 由 ASD（AeroSpace and Defence Industries Association of Europe）维护，前身是 1985 年的 AECMA 文档 PSC-85-16598。起草动因是欧洲航空公司需要非英语母语的机务也能一次读对维修手册。
- 现行版本 Issue 9，2025-01-15 发布。两部分：**53 条写作规则，分 9 节**；**词典**约 900 个批准词（一词一义、一词性），另有约 1200 个不批准词及其替换建议。
- 9 节：1 Words、2 Multi-word nouns、3 Verbs、4 Sentences、5 Procedural writing、6 Descriptive writing、7 Safety instructions、8 Punctuation and word count、9 Writing practices。
- 关键量化规则：操作句不超过 20 个词，描述句不超过 25 个词；一段不超过 6 句；多词名词不超过 3 个词；一句一个指令；操作文用祈使句；用主动语态；禁用分号（Rule 8.1）；动词只允许不定式、祈使式、一般现在时、一般过去时、一般将来时和作形容词的过去分词。
- ASD-STE100 是 ASD 的商标与版权作品。自 Issue 6（2013）起免费下载，官网 <https://www.asd-ste100.org/>。

## 三、与 STE 的映射

| STE 节 | 规则要点 | 本规范 |
| --- | --- | --- |
| 1 Words | 只用批准词，一词一义、一词性 | R1.1、R1.6 |
| 2 Multi-word nouns | 多词名词不超过 3 个词 | R2.8（中文改限制名词前的修饰语长度） |
| 3 Verbs | 只用批准动词形式，-ing 不作动词，不用短语动词 | R1.2、R1.7（中文无词形变化，改用「禁止名词化」） |
| 4 Sentences | 句长上限、一句一事、主动语态、祈使句、不靠省略成分缩短句子 | R2.1 到 R2.4 |
| 5 Procedural writing | 操作句 20 词内、祈使句、一步一动作、条件在前 | R2.3、R2.5、R4.1 |
| 6 Descriptive writing | 描述句 25 词内、一段一事、一段 6 句内 | R2.1、R3.1、R3.2 |
| 7 Safety instructions | 安全指令以明确的命令或条件开头 | R4.2 |
| 8 Punctuation and word count | 禁用分号（8.1）、字数计算（8.4 到 8.7） | R2.2（分号不算断句，等于要求拆句）、附录 A |
| 9 Writing practices | 短语动词、写法一致 | R1.1、R1.5 |

英文有、中文不需要的规则：动词形态限制（-ing、过去分词）、冠词、时态、词性限定。中文有、英文没有的规则见 [rules.md](./rules.md) 附录 B。

## 四、阈值来源

STE 的数字按英文的「词」算，不能直接换成中文的「字」。本规范采用 STC 在真实语料上的校准结果（未核验其原始数据，引用自其 README 与规范文档）：

- 语料：8 个开源项目的中文文档，2856 个文件，350 万字（TiDB、Kubernetes、MDN、Vue、Vite、Ant Design 的文档，加《Rust 程序设计语言》中文版、阮一峰 ES6 教程）。
- 好文档的句长分布：90% 的操作句不超过 33 字，90% 的描述句不超过 41 字。
- 本规范取 **操作句 30 字、描述句 40 字**。项目已有自己的阈值时，以项目为准。
- 字数算法见 [rules.md](./rules.md) 附录 A。
- R2.8 的 15 字没有校准，只是人工判断的参考值。

## 五、同类的中文项目

| 项目 | 管什么 | 与本 skill 的关系 |
| --- | --- | --- |
| [mzopedia/simplified-technical-chinese](https://github.com/mzopedia/simplified-technical-chinese)（STC，0.2） | 40 条编号规则、约 170 条受控词表、零依赖 Python 检查脚本、给 agent 的 SKILL.md | 同一思路的独立实现。本 skill 的规则集按 agent 输出重写，句长阈值引用它的校准数据；要逐条扫文件用它的 `tools/check.py` |
| [ruanyf/document-style-guide](https://github.com/ruanyf/document-style-guide) | 标题、段落、数值、标点、文档结构 | 互补。本 skill 不管排版 |
| [yikeke/zh-style-guide](https://github.com/yikeke/zh-style-guide) | 语言风格、标点、文档元素 | 互补 |
| [Fenng/Tech-Doc-Style-Chinese](https://github.com/Fenng/Tech-Doc-Style-Chinese) | 事实保真、改写流程、术语排版 | 互补。它明确不把句长做成硬规则，本 skill 做这部分 |

## 六、可选的检查工具

STC 的检查脚本零依赖，Python 3.9 以上：

```bash
git clone --depth 1 https://github.com/mzopedia/simplified-technical-chinese.git
python3 simplified-technical-chinese/tools/check.py 文档.md --kind 描述
```

它能查出禁用词、句长、段落句数、操作句里的被动与情态词、开放列举、相对日期。查不出事实错误、术语选得对不对、逻辑顺序。所有发现都要人工确认。本 skill 不内置脚本。

## 七、许可与免责

- 本 skill 的文本：MIT（同本仓库）。
- 规则集为自研，方法来自 ASD-STE100 的公开说明，句长阈值引用 STC 的校准结果（STC 规范文本 CC BY 4.0）。
- ASD-STE100 是 ASD 的商标。本 skill 与 ASD 无关，不声称符合 ASD-STE100。中文文本符合本规范，不代表符合 ASD-STE100。

## 八、已知局限

- 没有阅读理解对照实验。引用的是误报率校准，不是读者的理解速度和出错率。
- 词表约 120 条，只覆盖通用技术写作。项目术语应按项目自己的术语表处理。
- 规则里有几条只能人工判断：长定语、指代是否清楚、术语选得对不对、步骤里的警告与原因。
