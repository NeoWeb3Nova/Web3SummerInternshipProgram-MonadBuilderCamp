# Dev Builder 角色验证｜Neo

> 周次：Week 3｜从你的角色验证想法  
> 方向：Dev Builder  
> 日期：2026-07-20

---

## 1. 本周最需要完成的核心功能

**一条可演示的 swap 链路：自然语言意图 → Moss Capability 树 → simulate 验证 → UI 确认页 → 钱包签名。**

具体到代码层：

1. 接收用户自然语言输入（如“swap 100 USDC to MON on Monad”），解析成 `tokenIn`、`tokenOut`、`amountIn`。
2. 通过 Moss `registry.action("kuru", "swap", account, { tokenIn, tokenOut, amountIn, slippage })` 生成 Capability 树。
3. 通过 `createTraceSimulator(...).simulate(capability)` 执行模拟，获取 Receipts / Changes（如 Kuru Router Swap 事件、ERC-20 Transfer、授权等）。
4. 将 Receipt 结果翻译成 UI 可展示的确认信息：付出什么、收到多少、滑点、授权、风险提示。
5. 用户点击确认后，调用钱包签名（MetaMask / Rainbow / 等）并广播交易。

---

## 2. 可复用的现有工具、合约、SDK 或代码

### Moss 本地工程

| 资产 | 路径 | 说明 |
|------|------|------|
| Moss 仓库 | `experiments/moss/` | 已本地跑通 `pnpm install / build / test` |
| Kuru swap Capability | `packages/protocols/kuru/src/kuru.ts` | 已有 `swap` Capability，支持 `tokenIn/tokenOut/amountIn/slippage` |
| Kuru 测试 | `packages/protocols/kuru/test/kuru.test.ts` | 包含 mainnet e2e simulate 用例，可作为 Demo 参考 |
| 模拟器 | `packages/simulator/src/` | `createTraceSimulator` + `registry.parseReceipt` |
| MCP server | `packages/mcp-server/src/cli.ts` | 已有 `discover / load / action / simulate` 四个工具 |
| 示例脚本 | `pnpm --filter @themoss/example-simple-flow swap` | 可直接跑通 MON → USDC 的 simulate |

### 前端 / 钱包

| 资产 | 说明 |
|------|------|
| Vite + React | 小队熟悉，快速搭建 Demo UI |
| wagmi / viem | 连接钱包、签名、广播，Moss 本身也依赖 viem |
| Monad Testnet RPC | 可用 `https://rpc.monad.xyz` 或 `https://testnet-rpc.monad.xyz` |

### 之前的个人代码

- Neverland 适配器 PR：已经在子模块 `experiments/moss` 中做了 supply/withdraw Capability 和 simulate 测试。
- Cobo Agentic Treasury：有 React + wagmi + EOA 签名的前端经验，可复用钱包连接和签名广播逻辑。

---

## 3. 哪些功能暂时无法完成，需要简化或使用 Mock

### 真实开发部分

1. **Moss Capability 生成与 simulate**：直接复用 Kuru Protocol 的 `swap` Capability，返回 Capability 树和 Receipts。
2. **Receipt 解析**：从 simulate 结果中提取 `tokenIn`、`tokenOut`、`amountIn`、`amountOut`、`path`、`approval` 等关键信息。
3. **基础 UI 框架**：输入框 + 结果展示 + 确认按钮，连接钱包。
4. **测试网交易广播**：用户确认后通过 wagmi 签名并在 Monad testnet/mainnet 上留下交易哈希。

### Mock / 简化部分

| 原本想法 | 简化 / Mock 方案 | 原因 |
|----------|-------------------|--------|
| 真实自然语言 LLM 解析 | Demo 中用几个预置意图模板，点击后填充参数 | LLM 调用延迟、成本、并非本周核心 |
| 多个 DEX 路径比价 | 只用 Kuru 一家 | 模拟路径选择和协议适配器不在范围内 |
| 实时滑点计算 | 展示 quote 返回的 `estimatedAmountOut / minimumAmountOut` | 滑点计算由 Moss 内置，不需重复实现 |
| 自然语言输入的魔法参数抽取 | 用简单 regex / 确定性模板（如 “swap {amount} {tokenIn} to {tokenOut}”） | 将 LLM 不确定性隔离在 Demo 之外 |
| 钱包广播后的 on-chain Receipt 对账 | 做到签名广播即止，并展示 Explorer 链接 | 链上 Receipt 对账需要等待交易确认，超出本周边界 |

---

## 4. 技术方案简图

```text
┌─────────────────────────────────────────────────────────────┐
│  Frontend (Vite + React + wagmi/viem)                      │
│  ┌────────────────────────────────────────────────────────┐ │
│  │ 1. Intent Input          2. Confirmation UI       3. Wallet Sign │ │
│  └────────────────────────────────────────────────────────┘ │
├─────────────────────────────────────────────────────────────┤
│  Moss Backend (local or serverless function)                │
│  ┌────────────────────────────────────────────────────────┐ │
│  │  registry.action("kuru","swap", account, params)            │ │
│  │        ↓ Capability tree (approval + swap tx)            │ │
│  │  createTraceSimulator(...).simulate(capability)           │ │
│  │        ↓ Receipts / Changes                             │ │
│  │  parseReceipt(...) → human-readable outcome              │ │
│  └────────────────────────────────────────────────────────┘ │
├─────────────────────────────────────────────────────────────┤
│  Monad Network                                               │
│  - RPC: simulate via debug_traceCall                       │
│  - On-chain: Kuru Router, ERC-20 approvals                 │
└─────────────────────────────────────────────────────────────┘
```

---

## 5. 风险与缓解

| 风险 | 缓解 |
|------|------|
| Kuru mainnet 状态可能与测试不一致 | 首先使用离线 mock 验证 UI 流程，再切到 mainnet simulate |
| simulate 可能需要 funded account 或 state override | 使用随机非零地址作为 account，模拟器会用 state override 让账户拥有资产 |
| 钱包签名调试复杂 | 先做到“展示未签名交易并提供复制”，最后才连钱包广播 |
| Receipt 解析不稳定 | 从 Kuru 测试用例里复制已验证的 Changes 格式，做好 fallback |

---

## 6. 结论：这个想法能否完成

**可以完成。**

理由：
1. Moss `kuru.swap` Capability 和 simulate 已经在仓库中有可运行的 e2e 测试。
2. 前端 + 钱包签名的技术栈（Vite + React + wagmi）小队都熟悉。
3. 通过预置意图模板替代 LLM，可以在不引入外部依赖的情况下跑通 Demo。
4. 唯一的不确定性是 Kuru mainnet 当前流动性和 API 响应，但可以先用 mock / 离线测试保证 UI 链路，再在真实 RPC 上验证。

---

## 7. 我的检查结果如何影响团队接下来的计划

**以上 100 字说明**：

> Dev 验证结果：核心功能在技术上可行，Kuru swap Capability 与 simulate 已经在 Moss 仓库中验证。团队接下来应该：1）PM 立即锁定测试用户和测试任务；2）eleven 开始设计 3 屏确认页；3）Neo 今晚先用离线 mock 跑通一条 Kuru swap simulate，明天切到 mainnet RPC 留下 Demo Evidence。

---

## 关联文档

| 文档 | 路径 |
|------|------|
| 问题定义 | `submissions/week-03/problem-statement.md` |
| 团队介绍 | `submissions/week-03/team.md` |
| Idea Pitch | `submissions/week-03/idea-pitch.md` |
