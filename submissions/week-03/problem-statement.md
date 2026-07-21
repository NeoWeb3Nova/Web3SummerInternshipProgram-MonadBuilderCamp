# Problem & Mini Demo Card｜Moss Mini Demo Squad

> 周次：Week 3｜Day 2  
> 团队：Moss Mini Demo Squad  
> 成员：Neo（Dev）· Riso（PM）· eleven（UI）  
> 日期：2026-07-20

---

## 1. 目标用户

**第一次尝试 Monad 上 DeFi 的链上新手或轻量用户。**

特征：
- 已有钱包，知道如何签名
- 听说过 DEX / 借贷 / 流动性，但看不懂 ABI、合约地址、滑点、封装代币
- 对 AI Agent 感兴趣，但担心 Agent 自动转走资产或被恶意交易利用
- 想要一个**能理解、可验证、最终由自己确认**的交互方式

---

## 2. 核心问题

用户想用自然语言表达 DeFi 意图（例如“把 100 USDC 换成收益最高的稳定币”），但 Agent 经 Moss 返回的 Capability 交易树和 Receipts 充满他们不理解的 effects：

- 中间代币是什么？会不会被夹？
- 滑点、手续费、授权额度是多少？
- 这笔交易到底有没有风险？
- 我应该什么时候点确认？

结果是：**他们要么不敢点，要么误点，最终被 MEV / 滑点 / 恶意授权收割。**

---

## 3. 当前解决方式

| 方式 | 问题 |
|------|------|
| 直接进 DEX 手动操作 | 界面复杂、术语多、新手看不懂 |
| 使用通用 AI Agent | 不知道 Agent 会不会自动签名/广播，缺乏透明度 |
| 查文档 / 问社区 | 慢、碎片化、无法验证当前具体交易 |

用户真正缺的不是更多功能，而是一个**把复杂交易翻译成可理解、可验证、可拒绝的确认界面**的中间层。

---

## 4. 我们的方案

**自然语言意图 → Moss Agent 生成 Capability 树 → simulate 验证 effects（Receipts / Changes） → 用户理解后确认签名。**

本周只聚焦一条最小链路：

> **用户说“我想用 100 USDC 换 MON”，Agent 经 Moss action 返回一个 Swap Capability（包含未签名 TransactionNode），simulate 后展示 Receipt / Changes：token in / token out / 预估数量 / 滑点 / 授权状态，用户确认后签名。**

核心设计原则：
- **Moss 只规划与模拟，不自动签名、不自动广播**
- **所有关键 effects 必须在 UI 上用人话展示**
- **用户必须能一键拒绝或修改**

---

## 5. Mini Demo 核心功能

Demo 只展示以下 3 屏/3 步：

1. **意图输入**：用户输入一句自然语言（如“swap 100 USDC to MON on Monad”）
2. **Capability 解析与模拟**：Agent 经 Moss 调用 action 生成 Capability 树，simulate 后返回 Receipts / Changes
3. **确认页**：清晰展示 what / how much / risk / 授权 / 预估结果，用户确认后触发签名

Demo Evidence（周五前至少一种）：
- 可运行网页入口（本地或部署）
- 测试网交易哈希 / 合约地址
- 60–90 秒录屏

---

## 6. 本周明确不做

- 不接入多个协议 / 不比较多家 DEX
- 不实现自动执行、自动签名、自动策略
- 不托管用户私钥或助记词
- 不做多链、不做复杂投资组合管理
- 不做借贷/质押等需要多次交互的动作
- 不追逐“AI + Web3 超级应用”的完整叙事

---

## 7. 为什么适合 Monad

- **低延迟 + 高吞吐**：让“说完意图 → 秒级 simulate → 展示结果”的体验成立
- **EVM 兼容**：可直接复用现有 DEX / 预言机 / 标准合约
- **测试网可验证**：能留下真实交易哈希与合约地址作为 Demo Evidence

---

## 8. 关键假设与验证方式

**假设**：用户在看到“自然语言 → 可理解的 Capability 树 + simulate Receipts”后，更愿意确认并完成核心动作。

**验证方式**：
- Day 4 找 1–3 位同学试用 Demo
- 记录：是否看懂 Capability Receipt / 是否敢点确认 / 是否理解风险
- 根据反馈调整确认页信息层级

---

## 9. 团队分工

| 角色 | 本周任务 |
|------|----------|
| **Neo（Dev）** | 搭建前端框架、接入 Moss / simulate、准备 Demo Evidence |
| **Riso（PM）** | 控范围、维护看板、记录决策、准备用户测试问题 |
| **eleven（UI）** | 设计 3 屏主路径（输入 → Capability Receipt → 确认）、输出线框或高保真 |

---

## 10. 关联文档

| 文档 | 路径 |
|------|------|
| 团队介绍 | `submissions/week-03/team.md` |
| 组队提交卡 | `submissions/week-03/team-submission.md` |
| Team Formation Card | `submissions/week-03/team-formation-card.md` |
| Team Working Agreement | `submissions/week-03/team-working-agreement.md` |
| Idea Pitch | `submissions/week-03/idea-pitch.md` |
