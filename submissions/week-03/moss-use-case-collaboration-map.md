# Moss Demo 使用场景与协作地图｜Moss Mini Demo Squad

> 周次：Week 3｜Day 2  
> 团队：Moss Mini Demo Squad  
> 成员：Neo（Dev）· Riso（PM）· eleven（UI）  
> 日期：2026-07-20

---

## 具体用户场景

**小明是一名 DeFi 新手，有 MetaMask 钱包，想在 Monad 上用 100 USDC 买一点 MON。他看不懂 Kuru 的 orderbook 界面，也担心 AI Agent 会乱签名。**

他打开了本周 Mini Demo，想要一个能理解、可验证、自己控制的交易体验。

---

## User → Agent → Moss → Protocol 调用流程

```text
┌───────────────────────────────────────────────────────────────────────┐
│  1. User 输入意图                                             │
│     "swap 100 USDC to MON on Monad"                              │
├───────────────────────────────────────────────────────────────────────┤
│  2. Agent / Intent Parser                                        │
│     解析出 tokenIn=USDC, tokenOut=MON, amountIn=100             │
├───────────────────────────────────────────────────────────────────────┤
│  3. Moss Registry                                                │
│     registry.action("kuru", "swap", account, params)             │
│     → 返回 Capability 树（包含 approve + anyToAnySwap）            │
├───────────────────────────────────────────────────────────────────────┤
│  4. Moss Simulator                                               │
│     createTraceSimulator(...).simulate(capability)               │
│     → 返回 Receipts / Changes（Trade event, Transfer, RouterSwap） │
├───────────────────────────────────────────────────────────────────────┤
│  5. UI 确认页                                                   │
│     展示：付出 100 USDC / 收到 X MON / minimum out / 滑点 / 授权  │
│     用户点击确认                                              │
├───────────────────────────────────────────────────────────────────────┤
│  6. Wallet Sign & Broadcast                                     │
│     用户钱包签名 Capability 中的未签名交易，广播到 Monad 网络      │
└───────────────────────────────────────────────────────────────────────┘
```

---

## 三类角色交付物

### Research（Riso）

- **用户证据**：至少3 条证明 DeFi 新手看不懂交易信息的例子或调研。
- **竞品分析**：1–2 个现有解决方案（如通用 DeFi Agent、DEX 聚合器）的优缺点。
- **待验证问题**：新手是否真的愿意在看懂 Receipt 后签名？
- **反馈模板**：Day 4 用户测试问题和收集表。

### Ops（Riso + eleven）

- **一句话介绍**：用于招募测试者和 Demo Pitch。
- **测试者渠道**：至少3 个潜在渠道。
- **Demo 脚本**：3 分钟演示流程：问题 → 方案 → 演示 → 为什么 Monad → 下一步。
- **录屏素材**：Demo 录屏或截图。

### Dev（Neo）

- **可运行 Demo**：前端 + Moss 调用 + 钱包签名。
- **Demo Evidence**：交易哈希 / 合约地址 / 录屏 / README。
- **技术文档**：如何本地运行、哪些是 Mock、如何验证。

---

## 本周边界

- 只做 swap，不做借贷、质押、组合
- 只用 Kuru，不比价多家 DEX
- 只做一条主路径，不做错误恢复/取消后重来
- Moss 只做 simulate，不托管私钥，不自动签名

---

## 关联文档

| 文档 | 路径 |
|------|------|
| 问题定义 | `submissions/week-03/problem-statement.md` |
| Mini Demo 范围 | `submissions/week-03/mini-demo-scope.md` |
| Monad Fit | `submissions/week-03/monad-fit-card.md` |
| Build Plan | `submissions/week-03/build-plan.md` |
| Dev 验证 | `submissions/week-03/dev-role-validation.md` |
