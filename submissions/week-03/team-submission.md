# Week 3 团队组建提交

> 任务：组建 2–5 人团队，建立基础协作规则  
> 日期：2026-07-20  
> 状态：已组队（3 人）

---

## 团队名称

**Moss Mini Demo Squad**

---

## 团队成员与角色

| 角色 | 成员 | Track | 本周投入（预估） | 主要责任 |
|------|------|-------|------------|----------|
| **Dev / Tech Lead** | Neo | Tech | 25–30h | 合约、前端、Moss 整合、测试部署、Demo Evidence |
| **项目经理 PM** | Riso | Ops / Pitch | 待确认 | 范围、节奏、看板、决策记录、Pitch 结构 |
| **UI / 视觉** | eleven | Ops / 设计 | 待确认 | 信息架构、界面、演示路径、确认页可读性 |

### 角色分工说明

- **推进（PM / Pitch）：Riso**  
  负责进度推进、任务看板维护、每日 stand-up 纪要、范围决策与最终 Pitch 结构。
- **记录（PM + 全员协作）：**  
  Riso 主导文档沉淀；Neo 补充技术证据；eleven 补充界面与 Demo 录屏。
- **安全边界守卫（全员，技术决策由 Neo 拍板）：**  
  不托管用户私钥/助记词；Moss 路径只做规划与模拟，不自动签名/广播；涉及资产操作必须有明确确认步。

---

## 共同关注的问题

**链上 DeFi 新手在使用 AI Agent 执行意图时，因不理解 Capability 交易效果（Receipt 和 Changes）而签下风险操作。**

具体场景：新手用自然语言告诉 Agent “把 100 USDC 换成 MON”，Agent 经 Moss 返回一组 Capability（未签名交易树）和 simulate 后的 Receipt / Changes。但新手看不懂 effects（封装、滑点、中间代币、手续费、授权），容易误触或被 MEV 利用。

本周目标：做出一条可演示最小链路 —— 自然语言意图 → Moss Capability 树 + simulate → 用户可理解的确认界面，并留下 Demo Evidence（合约地址/交易哈希/可运行 Repo/录屏）。

---

## 目前缺少的角色

**暂无缺少核心角色；但缺少专职 Research Lead。**

- 问题论证、竞品分析、叙事论据目前由 **Riso（PM）主导 + Neo 补充技术论据**。
- 若后续扩展成 4 人团队，优先补充 Research Lead，专注用户调研与竞品分析。

---

## 协作规则概览

| 项 | 约定 |
|----|------|
| **团队群聊** | 微信群（建议命名：MBC-W3-MossMini） |
| **任务看板** | PM 在 Day 1–2 锁定 GitHub Projects 或 Notion |
| **每周同步** | 每日 21:00–21:15 UTC+8 stand-up，缺席前发异步三句（昨完/今计/卡点） |
| **任务分配** | 看板卡片包含：标题 · 负责人 · 截止日期 · 验收标准 · 关联文件/PR |
| **决策方式** | PM 主导范围决策，Dev 拍板技术路径，UI 拍板界面路径；安全边界任何人可一票否决 |
| **安全约定** | 不共享私钥、助记词或敏感信息；Demo Evidence 禁止编造 |

---

## 关联文档

| 文档 | 路径 |
|------|-------|
| 团队介绍 | `submissions/week-03/team.md` |
| Team Formation Card | `submissions/week-03/team-formation-card.md` |
| Team Working Agreement | `submissions/week-03/team-working-agreement.md` |
| Idea Pitch | `submissions/week-03/idea-pitch.md` |
