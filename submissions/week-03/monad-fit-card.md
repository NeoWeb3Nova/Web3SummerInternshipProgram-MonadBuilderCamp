# Monad Fit Card｜Moss Mini Demo Squad

> 周次：Week 3｜Day 2  
> 团队：Moss Mini Demo Squad  
> 成员：Neo（Dev）· Riso（PM）· eleven（UI）  
> 日期：2026-07-20

---

## 1. 为什么需要链上能力

DeFi 新手的痛点是**不信任链上操作**。这种信任问题只能通过链上可验证的机制缓解：

- **公开可审计的合约**：Kuru Router、ERC-20 approve 都是链上合约，用户可以核对目标地址。
- **模拟验证 effects**：在签名前通过 `debug_traceCall` 预览真实交易效果，这是传统 fintech 做不到的。
- **用户自持私钥**：Agent 只负责规划与模拟，最终签名权在钱包，这是链上原生的安全模式。
- **可留下证据**：交易哈希、合约地址、simulate 结果都能被独立验证，让“理解”不再是广告词。

---

## 2. 为什么适合 Monad

| Monad 特性 | 对本项目的意义 |
|------------|--------------|
| **低延迟 + 高吞吐** | “说完意图 → 秒级 simulate → 展示确认页”的体验在 Monad 上成立；如果 simulate 需要等很久，用户会认为 Agent 卡住了。 |
| **EVM 兼容** | 可以直接复用 Kuru（类 Uniswap V2/V3 的 DEX 精神）、ERC-20 标准、viem/wagmi 工具链，降低开发成本。 |
| **高性能低成本** | simulate 需要多次 RPC 调用（quote + traceCall），Monad 的低 gas 和高并发让“每次确认都 simulate”可以被普通用户承受。 |
| **开放测试网 + Explorer** | 能在 testnet 上留下真实交易哈希作为 Demo Evidence，导师/同学可以独立检查。 |
| **新生态的代理协议层（Moss）** | Moss 是 Monad 生态里专为 Agent 设计的协议层，本项目直接构建在这一原生能力上。 |

---

## 3. 待验证假设

| 假设 | 如何验证 |
|------|-----------|
| Monad mainnet RPC 能稳定支持 `debug_traceCall` | Neo 今晚用 mainnet RPC 跑一次 Kuru swap simulate，记录是否成功和耗时 |
| Kuru 当前有 USDC/MON 的流动性 | 通过 Kuru API quote 返回的 `path` 和 `estimatedAmountOut` 判断 |
| 新手能看懂 Capability Receipt 展示 | Day 4 用户测试收集反馈 |

---

## 4. 不适合 Monad 的地方（或需要缓解）

- **测试网状态不稳定**：若 mainnet simulate 不稳，先用离线 mock 保证 Demo 可演示，再切 mainnet。
- **新手可能没有 testnet 资金**：Demo 中用户只需观看，签名广播可选，不强求每人都真实发起交易。

---

## 5. 一句话 Monad Fit

> **在 Monad 上，用户可以用自然语言表达 swap 意图，在秒级 simulate 后看到可验证的交易效果，最终自己签名确认。**
