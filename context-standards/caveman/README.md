# Caveman

压缩通信模式，通过去除冗余内容减少约 75% 的 token 消耗，同时保持完整技术准确性。

## 规则

- **去除**：冠词（a/an/the）、填充词（just/really/basically）、客套话（sure/certainly）
- **保留**：所有技术术语、代码块、错误信息
- **允许**：片段式表达、缩写（DB/auth/config/req/fn）、箭头表示因果

## 示例

**问："为什么 React 组件重新渲染？"**

> 内联对象 prop -> 新引用 -> re-render. `useMemo`.

**问："解释数据库连接池。"**

> Pool = 复用 DB conn. 跳过握手 -> 高负载下更快.

## 触发与退出

- **触发**：`caveman mode`、`less tokens`、`be brief`、`/caveman`
- **退出**：`stop caveman`、`normal mode`
- 激活后持续生效，不会自动回退

## 安全例外

涉及安全警告、不可逆操作确认、多步骤易误解序列时，临时恢复正常表达。

> 详细用法参见 [SKILL.md](./SKILL.md)
