# Idea Pitch｜团队草案

> 周次：Week 3｜Builder Collaboration  
> 提出人：Neo（Dev）｜待与 PM / UI 对齐锁定  
> 日期：2026-07-20

---

## 一句话 Pitch

**为不想深耕合约和 ABI 的 DeFi 用户，做一个可以用自然语言提需求、Agent 在 Moss 安全边界内自动生成并验证 Capability 交易树、最后只剩下签名确认一步的 Mini Demo。**

---

## 术语说明

> Moss 2026-07 新架构（#31 Capability and Receipt framework）已用 **Capability tree + TransactionNode + Receipt** 替代旧的 `Plan / expects / planHash`。本文档使用新术语：
> - **Capability**：协议的一次写意图，拥有一个直接的未签名 TransactionNode 和一个 Receipt 解析器。
> - **TransactionNode**：Capability 树的叶子，包含一笔未签名交易。
> - **Receipt / Changes**：模拟后产生的有序原始事件与资产变化，Receipt 解析器将其翻译成可读文本。

---

## 为谁 · 解决什么 · 准备做什么

| 要素 | 内容 |
|------|------|
| **为谁** | 已有钱包、想试 Monad 上 DeFi，但被 ABI / 合约 / 滑点 / 授权吓退的新手或轻量用户 |
| **什么问题** | 看不懂 DApp 操作路径；担心 Agent 自动转走资产；不知道何时该签名、如何确认 Capability 安全 |
| **准备做什么** | 自然语言 → Agent 解析 → Moss 生成 Capability 树 + simulate → UI 清晰展示 Receipt / Changes → 用户确认签名 |
| **本周边界** | 只验证 **一条** 核心动作（Swap / Lending 查询或存入 / Portfolio 只读 三选一） |

---

## 为什么现在做、为什么我们能做

1. **Dev 已有 Moss 证据链**：本地全流程、适配器草稿、Neverland PR、Core PR #36。  
2. **Monad Fit**：低延迟高吞吐，让「说完意图 → 马上看到 Capability 树与 simulate Receipts」在体验上成立。
3. **安全叙事清晰**：Moss 不签名、不发送；Receipts 和 Changes 必须与用户原意对齐——正好对上「Agent 信任」痛点。
4. **三人分工刚好盖住最小交付**：Dev 出可跑链路 + 链上证据；PM 控范围与节奏；UI 让确认页可被 3 分钟讲懂。

---

## 本周要验证的关键假设

> 用户在看懂「自然语言 → Capability 树 + simulate Receipts」之后，愿意继续点确认并完成（或模拟完成）核心动作。

---

## 团队内角色与 Pitch 分工

| 角色 | Pitch 中负责 |
|------|----------------|
| **PM** | 用户故事、范围一句话、本周做到什么程度 |
| **Dev（Neo）** | 技术路径、Moss 安全边界、Demo Evidence |
| **UI** | 关键界面流程（输入 → 结果 → 确认）、演示观感 |

---

## 可能的 Demo 形态（与 UI 共定）

| 形态 | 说明 | 优先级建议 |
|------|------|------------|
| 简单网页 | 输入框 + Capability/simulate Receipts 展示 + 确认按钮 | **首选**（利于 UI 发挥 + 录屏） |
| CLI / Bot | 终端返回 Capability 树与 simulate Receipts | 后备 / Dev 先打通逻辑 |
| 录屏 | 完整链路 60–90 秒 | 必交展示材料 |

---

## 待团队锁定（Day 2）

- [ ] 核心动作最终选哪个（Swap / Lending / Portfolio）  
- [ ] 目标用户一句话是否改写  
- [ ] UI 主路径线框（3–5 屏内）  
- [ ] 「本周做到什䣇度」共同预期写入 Solution Design / Build Plan
