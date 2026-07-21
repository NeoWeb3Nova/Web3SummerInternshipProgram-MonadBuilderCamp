# Mini Demo Scope｜Moss Mini Demo Squad

> 周次：Week 3｜Day 2  
> 团队：Moss Mini Demo Squad  
> 成员：Neo（Dev）· Riso（PM）· eleven（UI）  
> 日期：2026-07-20

---

## 核心用户动作

**用户输入一句自然语言 swap 意图，经 Moss 生成 Capability 树并 simulate 验证后，在可理解的确认页上点击签名。**

具体动作：`swap 100 USDC to MON on Monad`

---

## Must Have（本周必须做到）

1. **意图输入**：用户能输入/选择一句 swap 意图。
2. **Moss Capability 生成**：通过 Kuru `swap` Capability 生成未签名交易树。
3. **simulate 验证**：运行模拟，获取 Receipts / Changes。
4. **确认页**：展示 token in / token out / estimated out / minimum out / slippage / approval / risk，用户能确认或取消。
5. **钱包签名**：用户确认后触发钱包签名（至少展示待签名交易，最好广播）。
6. **Demo Evidence**：至少一种可检查产出（可运行网页、测试网交易哈希、60–90 秒录屏）。

---

## Nice to Have（有余力再做）

1. 多个预置 swap 意图模板（如 "swap 1 MON to USDC"）。
2. 实时 quote 数据展示。
3. 手机端适配的确认页。
4. 更多风险提示（如 price impact、MEV 风险）。
5. 录屏配音或动画过渡。

---

## Not This Week（明确不做）

- 不接入多个 DEX 或多个协议（只用 Kuru）
- 不实现自动执行 / 自动签名 / 自动策略
- 不托管用户私钥或助记词
- 不做多链、不做借贷 / 质押 / 多次交互
- 不追逐 "AI + Web3 超级应用" 完整叙事
- 不用真实 LLM 做自然语言解析（用预置模板）
- 不做链上 Receipt 事后对账（Demo 做到广播为止）

---

## 关键假设

**用户在看到“自然语言 → Capability 树 + simulate Receipts → 可理解确认页”后，愿意点击确认并完成签名。**

---

## 为什么只选 swap

- Kuru 是 Moss 仓库中已有的 Protocol ，Capability 和 Receipt 验证过
- Swap 是 DeFi 新手最容易理解的“换钱”动作
- 只需要一次用户交互，适合 3 分钟 Demo
- 能在 UI 上清晰展示 effects（付出什么、收到多少、滑点、授权）

---

## 验收标准

- [ ] 用户能在 30 秒内输入/选择意图
- [ ] Capability / simulate 结果能在 5 秒内返回
- [ ] 确认页能让非技术用户看懂 "我在付出什么，收到什么"
- [ ] 用户点击确认后能触发钱包签名（或展示待签名状态）
- [ ] 能提供一种 Demo Evidence
