# Week 3 组队招募文案

> 适用场景：微信群 / Discord / Telegram  
> 方向：Moss-powered DeFi Agent Mini Demo  
> 作者：Neo

---

## 版本一：简短版（推荐发微信群）

```
🚀 Week 3 找队友｜Moss-powered DeFi Agent Mini Demo

我是 Neo，Week 2 选的 Dev Builder。已本地跑通 Moss（discover→load→action→simulate），写了 MockVault 适配器草稿，还给 Moss 上游提交了 PR #36。

想在 Week 3 做一个超小 Demo：
用自然语言说 "把 1 MON 换成 USDC"→Agent 解析→Moss 生成 Capability 树→simulate 验证→只剩签名确认。
只验证一条核心链路，不做通用 Agent，不做多链。

找 2–3 位队友：
• Research / Product：定义目标用户、竞品、风险边界
• Ops / 叙事 / 设计：Landing Page、测试任务、3 分钟 Pitch
• 另一 Dev（可选）：前端 / 合约 / Moss 适配器

我本周可投入 25–30h，能做合约、前端、Moss 调用和模拟。

有兴趣的朋友直接私我，附上你的方向和本周时间。
GitHub：https://github.com/NeoWeb3Nova
```

---

## 版本二：详细版（推荐发 Discord / 论坛）

```
🎯 Week 3 Team Matching｜Looking for Research + Ops + Dev teammates

Hi，我是 Neo，这次 Builder Camp 的 Dev Builder（Tech）。

**我的 Week 2 Proof of Work**
- 本地跑通 nishuzumi/moss：install / build / test / wmon-wrap 示例全通过
- 逐行阅读 core / simulator / _template / wmon.ts，输出学习笔记
- 实现可编译、可测试的 MockVault 适配器草稿
- 向 Moss 上游提交了第一个 PR：#36（修复 uint unsafe number 问题）
- Monad Testnet 已完成合约部署（交易哈希已验证）

**想做的 Mini Demo**
一个 Moss-powered 的 DeFi Agent 最小可用原型：
自然语言意图 → Agent 解析 → Moss 生成 Capability 树 → simulate 验证 effects → 用户确认签名

只选一个核心动作，例如：
- Swap Assistant："1 MON → USDC"
- Lending Assistant：查询或执行 deposit
- Portfolio Assistant：读取余额与仓位摘要

**安全边界**
- Moss 只模拟，永远不签名不发送交易
- 涉及资产的操作必须保留人工确认
- 只做一条链路，不做自动策略 / 多协议聚合

**找什么样的队友**
1. Research / Product：确认目标用户、竞品、协议风险、Monad Fit
2. Ops / Narrative / Design：Landing Page、用户测试、Demo Story、Pitch
3. Dev（可选）：前端 / 合约 / Moss adapter，能独立负责一个模块

**时间投入**
- 我本周可投入 25–30h
- 偏好每日 21:00–22:00 UTC+8 Stand-up（可协商）
- 工具：GitHub Issues/Projects + 微信/Telegram + Notion

**联系我**
- GitHub：https://github.com/NeoWeb3Nova
- 个人主页：https://amshe.fun
- 微信：Web3-Nova-Neo（添加时请备注：Monad Builder Camp + 方向）
- Moss PR：https://github.com/nishuzumi/moss/pull/36
- 直接回复或私聊，附上：你的方向 / 本周可投入时间 / 感兴趣的 Demo 方向

让我们先用一个 Mini Demo 合作一次，然后决定是否一起进入 Week 4 Hackathon 💪
```

---

## 版本三：针对已有 Moss 基础的同学

```
💚 找 Moss 搭子｜Week 3 一起做个可演示的 Agent Demo

我是 Neo，Week 2 深度搞了 Moss，也是一个把 AI 员工付钱这件事做到黑客松台上的 Builder：
- 刚在 AI × Web3 School Agentic Hackathon / Cobo Agentic Wallet Track 拿下**季军**——项目是「一人公司的 AI 员工财务操作系统」，把 Cobo Pact 抽象成 AI 员工虚拟支出卡，设置预算、限额、白名单、审计规则
- 本地跑通 Moss 全流程，有 MOSS-STUDY-NOTES 和 MockVault adapter 草稿
- 给 Moss core 提交了 PR #36（uint unsafe number fix）
- 也写了两篇公众号文章

找同样对 Moss / Agent × DeFi 感兴趣的搭子，在 Week 3 做一个可 Demo 的端到端流程。

最想要：
- 一位 Research / Product：定义真实场景、用户、协议风险
- 一位 Ops / 叙事：把技术流程转成用户能懂的 Demo Story

Dev 也欢迎，特别是熟悉前端或已经看过 Moss 源码的同学。

我本周 25–30h，可以做 core dev + 部分 research/ops。

**联系我**
- 微信：Web3-Nova-Neo（备注：Monad Builder Camp + 方向）
- 个人主页：https://amshe.fun
- GitHub：https://github.com/NeoWeb3Nova
- Cobo 赛道季军项目：https://github.com/NeoWeb3Nova/opc-agent-treasury/blob/master/PROPOSAL.md
- Moss PR：https://github.com/nishuzumi/moss/pull/36

有兴趣直接加我微信或私聊，我们快速约个 15 分钟语音对齐一下。
```

---

## 使用建议

| 场景 | 推荐版本 | 理由 |
|------|---------|------|
| 微信群 | 版本一 | 信息密度高，一屏能看完，不占用公庆 |
| Discord / 论坛 | 版本二 | 信息完整，方便后续搜索和跳转 |
| 针对 Moss 已有基础者 | 版本三 | 快速建立共同语言，减少重复解释 |

---

## 发出后的跟进

1. 发出后 2 小时内，统计回复人数。
2. 对每个回复，问 3 个问题：方向、时间、兴趣点。
3. 若兴趣匹配，立即约 15 分钟语音，讨论：
   - 是否对同一个问题感兴趣
   - 时间投入是否匹配
   - 每日同步时间
   - 各自能贡献什么
4. 语音后若决定组队，当天完成 Team Formation Card 和 Team Working Agreement。
