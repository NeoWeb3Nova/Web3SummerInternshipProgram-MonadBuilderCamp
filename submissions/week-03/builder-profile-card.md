# Builder Profile Card｜Neo

> 周次：Week 3｜Builder Collaboration  
> 角色：Dev Builder（Tech / Core Dev）  
> 日期：2026-07-20（组队确认后更新）  
> 状态：**已组队**｜3 人小队（Dev + PM + UI）

---

## 1. 我是谁

| 字段 | 内容 |
|------|------|
| **姓名 / 代号** | Neo |
| **主方向** | Dev Builder（Tech / Core Dev） |
| **次方向** | 可兼任 Research（协议调研、风险分析）与技术叙事 |
| **时区** | UTC+8，晚间协作 |
| **本周可投入时间** | 工作日 3–4h/天，周末 6–8h/天，合计约 **25–30h** |
| **团队角色** | 技术方案、合约 / 前端 / Moss 调用、模拟验证、Demo Evidence |

---

## 2. Week 2 Proof of Work

| 证据 | 路径 / 链接 | 说明 |
|------|-------------|------|
| Moss 本地跑通 | `experiments/moss/` | `pnpm install / build / test`；跑通 `wmon-wrap` |
| 深度学习笔记 | `experiments/moss/MOSS-STUDY-NOTES.md` | core / simulator / _template / wmon |
| MockVault 适配器草稿 | `experiments/moss/packages/protocols/mockvault/` | 可编译、可测试的协议适配器学习草稿 |
| Neverland 适配器 PR | [NeoWeb3Nova/moss#1](https://github.com/NeoWeb3Nova/moss/pull/1) | supply / withdraw / accountData |
| Moss Core 开源 PR | [nishuzumi/moss#36](https://github.com/nishuzumi/moss/pull/36) | 修复 `uint` unsafe JavaScript number |
| 公众号文章 × 2 | `moss-wechat-article.md` / `moss-beginner-guide.md` | 开发者深度文 + 新手教程 |
| Role Statement | `week-2-role-statement.md` | Tech / Core Dev 定位 |
| 链上基础 | `submissions/week-01/mini-demo-0.md` | Monad Testnet 钱包、RPC、合约部署 |
| Cobo 黑客松季军 | [opc-agent-treasury](https://github.com/NeoWeb3Nova/opc-agent-treasury/blob/master/PROPOSAL.md) | AI 员工财务操作系统 / Pact 虚拟支出卡 |

---

## 3. 我能为团队贡献什么

### Dev 核心
- 智能合约：Solidity + Foundry（编写、测试、部署脚本）
- 前端与链上交互：Vite + React + wagmi / viem
- Agent × 协议：Moss action、Capability 树、simulate 验证
- 最小 PoC 快速验证，再决定是否扩大开发
- Demo Evidence：合约地址、交易哈希、Explorer、可复现 README

### 可兼任
- **Research 辅助**：ABI 来源核查、风险边界、Monad Fit
- **Pitch 技术段**：架构说明、安全边界、为什么适合 Monad

### 我不单独扛的部分（已有队友）
- 产品范围控制与进度推进 → **PM**
- 界面体验与视觉表达 → **UI**

---

## 4. 队友需求（已匹配）

| 需求 | 状态 | 对应角色 |
|------|------|----------|
| 推进与记录、范围控制 | ✅ 已找到 | 项目经理（PM） |
| 界面 / 演示体验 | ✅ 已找到 | UI |
| 另一位 Dev | 本周可选，非必须 | — |

### 协作期待（个人侧）
- 直接沟通、快速决策，用测试与反馈修正方案
- 每日短同步 + 任务看板实时更新
- Demo 先做**一条能演示的最小链路**，再迭代

---

## 5. 我最想解决什么问题

**首选：Moss-powered DeFi Agent Mini Demo**

用户用自然语言提出 DeFi 意图 → Agent 经 Moss 生成 Capability 树 → simulate 验证 Receipts / Changes → **人签名确认**。

本周只验证一个核心动作（三选一，与 PM 对齐后锁定）：

1. **Swap Assistant**：自然语言换币 → Capability 树 → simulate → 确认  
2. **Lending Assistant**：查询 / 存入（Neverland 等）  
3. **Portfolio Assistant**：余额与仓位摘要（只读优先）

**安全边界（不可妥协）**  
Moss 不签名、不广播；有资产操作必须人工确认；不做自动策略 / 多链。

---

## 6. 60 秒自我介绍

>我是 Neo，Dev Builder。Week 2 主攻 Moss：本地跑通 discover → load → action → simulate，写了 MockVault 草稿，Neverland 适配器与 Core PR #36 都已提交；另外在 Cobo Agentic Wallet Track 拿过季军。我在小队里负责合约、前端、Moss 调用和可检查的 Demo Evidence。我想做的是：让用户用自然语言表达 DeFi 意图，Agent 在 Moss 安全边界内生成 Capability 树并模拟，最后只剩签名一步。本周大约 25–30 小时，偏好每晚短同步，先砍到一条可演示链路再冲 Week 4。

---

## 7. 联系与协作

| 项 | 内容 |
|----|------|
| GitHub | https://github.com/NeoWeb3Nova |
| 主页 | https://amshe.fun |
| 微信 | Web3-Nova-Neo |
| 协作工具 | 见 `team-working-agreement.md` |
| 每日同步 | 默认 21:00–21:15 UTC+8（团队可改） |

---

## 8. 本周目标（个人 checklist）

- [x] Day 1：Builder Profile + Idea Pitch + 组队 + Working Agreement
- [ ] Day 2：Problem & User Card、Mini Demo Scope、Monad Fit、Build Plan（Solution Design）
- [ ] Day 3：Research / Ops / Dev Handoff，跑通或模拟一条端到端链路
- [ ] Day 4：3–5 人测试，Feedback Log + 至少一次迭代
- [ ] Day 5：Mini Demo + 3 分钟 Pitch + Hackathon Readiness
