# 简明技术中文（STE-zh）

用中文写技术内容时默认生效的受控写作规范。方法借鉴航空业的 **ASD-STE100**（Simplified Technical English，简化技术英语），按中文的歧义来源重写：名词化结构、长定语、「以上」的端点、「可以」的许可与能力、省略主语、开放列举。

目标一句话：**读者读一遍就不会读错。**

## 触发与退出

- **默认生效**：写中文技术内容时自动按本 skill 写，不必等用户触发。
- **手动触发**：`简明技术中文`、`STE-zh`、`受控中文`、`一词一义`、`严格模式`，或要求中文内容「别有歧义」「写清楚」「按 STE 写」。
- **严格模式**：连【建议】级规则一起执行。
- **退出**：说「停止 STE-zh」「不用简明技术中文」，本会话停用。
- 优先级：系统与用户明确指令 > 用户指定的输出格式 > 项目自带的写作规范 > 本 skill。

## 结构

SKILL.md 只留入口与底线，细则分 5 个模块按需加载：

| 文件 | 说明 |
|------|------|
| [`SKILL.md`](SKILL.md) | 入口：生效与退出、适用范围、三条底线、必须级索引、发送前自检、禁区 |
| [`references/rules.md`](references/rules.md) | 7 节 47 条完整规则，分【必须】/【建议】，每条带不批准/批准例句，附字数算法 |
| [`references/vocab.md`](references/vocab.md) | 受控词表：禁用词与替换、情态词与强度、选词表、一词一义限定、行业黑话 |
| [`references/compose.md`](references/compose.md) | 与 i-have-adhd（结构层）、caveman（压缩层）的三层分工、裁决顺序、不可压缩清单 |
| [`references/examples.md`](references/examples.md) | 六组五种写法对照，含压缩压坏的反例与修复 |
| [`references/sources.md`](references/sources.md) | 来源（ASD-STE100 Issue 9 事实）、与 STE 九节的映射、阈值出处、同类项目、局限与许可 |

## 与 i-have-adhd、caveman 组合

三个 skill 可以同时开。句式层（本 skill）一直生效，另两层按需叠加。

| 层 | 管什么 | 来源 |
|----|--------|------|
| 结构层 | 首行给下一步行动、多步工作编号、跨轮重述状态 | `i-have-adhd` |
| 句式层 | 句长上限、一句一事、祈使句、主动句、条件在前、一词一义 | 本 skill |
| 压缩层 | 删虚词与铺垫、片段化、箭头表因果 | `caveman` |

裁决顺序：安全与不可逆操作 > 事实与模态保真 > 歧义消除 > 可扫读结构 > 压缩。**压缩永远输给前四条**；中文里删否定、执行者、条件、模态词会改意思，不可压缩清单见 [compose.md](references/compose.md)。

## 运行机制

- 靠 Agent 遵守上下文中的指令生效，没有程序强制执行。
- 极长会话或上下文压缩（compaction）后 Agent 可能遗忘规则。发现写法退化，重新说一次「简明技术中文」即可恢复。
- 希望每个会话默认开启，把这条写进全局规则文件（例如 `~/.claude/CLAUDE.md`、`AGENTS.md`）。

## 来源与许可

- 方法来自 ASD-STE100 的公开说明；规则集、词表与阈值按中文场景自研，不是原文直译。
- 句长阈值（操作句 30 字、描述句 40 字）引用 [mzopedia/simplified-technical-chinese](https://github.com/mzopedia/simplified-technical-chinese) 在真实语料上的校准结果。
- 「事实与证据」（R7）参考 [dualface/ste-zh](https://github.com/dualface/ste-zh) 的验证状态要求，按中文文档场景改写。
- 与 ASD 组织无隶属关系，不声称符合 ASD-STE100。文本许可：MIT。
- 已知局限：没有阅读理解对照实验；词表约 120 条；长定语、指代、术语选择、步骤里的警告与原因只能人工判断；不内置检查脚本。
