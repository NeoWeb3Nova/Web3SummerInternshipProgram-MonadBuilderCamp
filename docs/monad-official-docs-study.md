# Monad 官方技术文档学习基准

## 来源

- 技术文档：<https://docs.monad.xyz/llms-full.txt>
- 本地快照：`monad-llms-full.txt`
- 快照体量：1,680,051 chars / 40,495 lines
- SHA256：`20c72aa6ccb13b9857b541d67ecefd42bb5b0098474413a43c511c7edb6f0ee7`

> 本次 Monad Builder Camp 学习计划后续以该官方文档为技术事实基准。若与口述分享、旧文章或通用 EVM 经验冲突，优先回到该文档核对。

---

## 学习计划中必须覆盖的技术主线

### 1. Network / Chain 基础信息

- Monad Mainnet：Chain ID `143`，币种 `MON`。
- Mainnet 公共 RPC 包括：
  - `https://rpc.monad.xyz` / `wss://rpc.monad.xyz`
  - `https://rpc1.monad.xyz` / `wss://rpc1.monad.xyz`
  - `https://rpc2.monad.xyz` / `wss://rpc2.monad.xyz`
  - `https://rpc3.monad.xyz` / `wss://rpc3.monad.xyz`
  - `https://rpc-mainnet.monadinfra.com` / `wss://rpc-mainnet.monadinfra.com`
- 浏览器：MonadVision、Monadscan。
- 学习任务涉及地址、RPC、代币、桥、AA、Safe、Multicall 等，必须回查官方文档，不凭记忆填写。

### 2. Monad vs Ethereum 的关键差异

学习时要特别强调：Monad 是 EVM 兼容，但不是“和以太坊完全一样”。需要单独理解：

- 交易按 `gas_limit` 收费，而不是只按实际 gas used 收费。
- 动态 base fee 控制逻辑与以太坊不同。
- opcode pricing 有 Monad 特化差异，尤其 cold state access 和 precompile 成本。
- block states / finality / real-time data 与 Ethereum 心智模型不同。
- historical state lookup、RPC 方法限制、batch call limit、provider 差异都可能影响前端和脚本。

### 3. 高性能应用最佳实践

技术训练不能只做 HelloWorld；要训练 Monad 高吞吐环境下的工程习惯：

- 静态 gas 场景可硬编码 gas limit，避免不必要的 `eth_estimateGas`。
- 多个 `eth_call` 应考虑并发请求、batch call 或 Multicall。
- read-heavy / historical / activity feed 场景不要反复 `eth_getLogs`，应使用 indexer。
- 高频发送交易时要本地管理 nonce。
- 多笔交易可以并发提交，但要理解 mempool、nonce、receipt、finality 的生命周期。

### 4. 合约开发与部署

学习计划中合约部分应覆盖：

- Foundry / Monad Foundry 部署流程。
- Hardhat 部署流程。
- Remix 基础部署。
- 合约验证流程。
- canonical contract addresses。
- 128KB 合约大小限制相关差异。
- EIP-7702、ERC-4337、Permit2、Safe、Multicall3 等常用基础设施地址的使用边界。

### 5. Gas / Opcode / Reserve Balance

这是 Monad 学习区别于普通 EVM 学习的核心模块：

- Gas pricing：gas limit 收费、base fee controller、开发者设置 gas limit 的建议。
- Opcode pricing：cold access、precompile 等成本变化对合约设计的影响。
- Reserve balance：为什么需要、参数、完整机制、调节方法、对交易有效性和账户余额判断的影响。

### 6. 架构理解

Research / 技术文章任务应围绕：

- MonadBFT。
- Asynchronous execution。
- Parallel execution。
- MonadDB。
- JIT Compilation。
- RaptorCast。
- Blocksync / Statesync。
- Block states：Proposed、Voted、Finalized、Verified。
- Transaction lifecycle：submission → mempool propagation → block inclusion → propagation → local execution → query outcome。

### 7. 数据读取与索引

项目型学习要覆盖：

- JSON-RPC API 差异与限制。
- WebSocket subscriptions。
- `eth_sendRawTransactionSync`。
- `eth_getLogs` 使用边界。
- Envio HyperIndex、GhostGraph、Goldsky、QuickNode Streams、Allium 等索引方案。
- Execution Events / real-time data：只在需要极低延迟、节点级数据能力时深入。

### 8. 前端与钱包集成

前端任务应覆盖：

- Add Monad to Wallet / Mainnet / Testnet 配置。
- Wallet Developer Integration Guide。
- Reown AppKit、Privy、Thirdweb、React Native / PWA 模板等。
- gas handling、transaction lifecycle、simulation/RPC differences。
- 钱包支持状态需要从官方 Tooling & Infrastructure 表核对。

### 9. 生态和应用方向

可转化成学习项目的官方 guide：

- donation blink。
- custom stablecoin with Brale。
- ERC-7730 clear signing。
- ERC-8004 trustless agents。
- x402-enabled endpoint with Monad support。
- portfolio viewer using Moralis。
- Kuru Flow swaps。
- Farcaster Mini App。
- MCP server interacting with Monad Testnet。

---

## 后续使用规则

1. 制定学习计划、任务卡、作业或 demo 时，先从本文件确定主题，再回查 `monad-llms-full.txt` 对应章节。
2. 写任何链参数、合约地址、RPC URL、工具支持状态前，必须从官方快照或在线文档确认。
3. 技术解释采用“概念 → 为什么 Monad 需要它 → 与以太坊差异 → 开发者应该怎么做 → 小实验验证”的结构。
4. 对新手任务，先让学员跑通钱包/RPC/一笔交易/HelloWorld；对进阶任务，重点转向 gas、indexer、并发交易、实时数据和 agentic payments。
