# Problem & Mini Demo Card｜Moss Mini Demo Squad

> 周次：Week 3｜Day 2  
> 团队：Moss Mini Demo Squad  
> 成员：Neo（Dev）· Riso（PM）· eleven（UI）  
> 日期：2026-07-20

---

## 提交模板

### 目标用户

**第一次尝试 Monad 上 DeFi 的链上新手或轻量用户。**

特征：已有钱包、知道如何签名；听说过 DEX / 借贷 / 流动性，但看不懂 ABI、合约地址、滑点、封装代币、授权额度；对 AI Agent 感兴趣，但担心 Agent 自动转走资产或被恶意交易利用。

---

### 核心问题

用户想用自然语言表达 DeFi 意图（例如“把 100 USDC 换成 MON”），但 Agent 经 Moss 返回的 Capability 交易树和 Receipts / Changes 充满他们不理解的效果：中间代币是什么、滑点和手续费多少、授权额度意味着什么、这笔交易到底有没有风险。结果是：他们要么不敢点确认，要么误点，最终被 MEV / 滑点 / 恶意授权收割。

---

### 当前解决方式

- **直接进 DEX 手动操作**：界面复杂、术语多、新手看不懂每一步在做什么。
- **使用通用 AI Agent**：不知道 Agent 会不会自动签名/广播，缺乏透明度和可验证性。
- **查文档 / 问社区**：慢、碎片化、无法验证当前具体交易的真实效果。

---

### 我们的方案

**自然语言意图 → Moss Agent 生成 Capability 树 → simulate 验证 effects（Receipts / Changes） → 用户在可理解的确认页上签名。**

Moss 新架构（#31 Capability and Receipt framework）中：
- **Capability**：协议的一次写意图，拥有一个直接的未签名 TransactionNode 和一个 Receipt 解析器。
- **TransactionNode**：Capability 树的叶子，包含一笔未签名交易。
- **Receipt / Changes**：模拟后产生的有序原始事件与资产变化，Receipt 解析器将其翻译成可读文本。

我们利用这一层，把复杂的链上交易效果翻译成普通人能看懂的确认信息，并把最终签名权牢牢留给用户。

---

### Mini Demo 核心功能

只做 **一条** 可演示链路：

> 用户输入“swap 100 USDC to MON on Monad” → Agent 经 Moss `action` 生成 Swap Capability 树 → `simulate` 返回 Receipts / Changes → UI 展示 token in / token out / 预估数量 / 滑点 / 授权状态 / 风险提示 → 用户确认后触发钱包签名。

Demo 只展示 3 屏：
1. **意图输入屏**：自然语言输入框
2. **Capability / simulate 结果屏**：展示 Capability 树结构和 Receipt 文本
3. **确认屏**：关键 effects 一目了然，用户可确认或拒绝

Demo Evidence（周五前至少一种）：可运行网页入口、测试网交易哈希 / 合约地址、60–90 秒录屏。

---

### 本周不做

- 不接多个协议 / 不比较多家 DEX
- 不实现自动执行、自动签名、自动策略
- 不托管用户私钥或助记词
- 不做多链、不做复杂投资组合管理
- 不做借贷/质押等需要多次交互的动作
- 不追逐“AI + Web3 超级应用”的完整叙事
- 不保留旧架构 Plan / expects / planHash 概念

---

## 补充信息

### 为什么适合 Monad

- **低延迟 + 高吞吐**：让“说完意图 → 秒级 simulate → 展示结果”的体验成立
- **EVM 兼容**：可直接复用现有 DEX / 预言机 / 标准合约
- **测试网可验证**：能留下真实交易哈希与合约地址作为 Demo Evidence

### 关键假设与验证方式

**假设**：用户在看到“自然语言 → 可理解的 Capability 树 + simulate Receipts”后，更愿意确认并完成核心动作。

**验证方式**：Day 4 找 1–3 位同学试用 Demo，记录是否看懂 Capability Receipt、是否敢点确认、是否理解风险，并根据反馈调整确认页信息层级。

### 团队分工

| 角色 | 本周任务 |
|------|----------|
| **Neo（Dev）** | 搭建前端框架、接入 Moss `action` / `simulate`、准备 Demo Evidence |
| **Riso（PM）** | 控范围、维护看板、记录决策、准备用户测试问题 |
| **eleven（UI）** | 设计 3 屏主路径（输入 → Capability Receipt → 确认）、输出线框或高保真 |

### 关联文档

| 文档 | 路径 |
|------|------|
| 团队介绍 | `submissions/week-03/team.md` |
| 组队提交卡 | `submissions/week-03/team-submission.md` |
| Team Formation Card | `submissions/week-03/team-formation-card.md` |
| Team Working Agreement | `submissions/week-03/team-working-agreement.md` |
| Idea Pitch | `submissions/week-03/idea-pitch.md` |
