# Monad ERC-8004 技术文档学习笔记

## 来源

- 官方文档：<https://docs.monad.xyz/guides/erc-8004#how-to-register-and-build-with-erc-8004-trustless-agents-on-monad>
- 官方文档在 `llms-full.txt` 中的 source：<https://docs.monad.xyz/guides/erc-8004>
- 本地源码快照：`docs/monad-erc-8004-guide-source.md`
- 快照体量：7,393 chars / 231 lines
- SHA256：`b0950f29f1e9fe1dc9175d915d9ba62e70786a04fdb5b8504f9cad0fd8bfcd4b`

---

## 1. ERC-8004 是什么

ERC-8004 是 Ethereum standard for Trustless Agents。

它给 AI agents、agentic services、MCPs、APIs 等提供三类链上注册表：

1. Identity Registry：代理身份。
2. Reputation Registry：代理交互后的不可变反馈。
3. Validation Registry：第三方验证代理工作结果，目前文档标记为 coming soon。

核心目的：让 AI agent 变成可发现、可支付、可审计、可验证的经济主体。

---

## 2. 关键收益

### Portable Identity

Agent 通过 ERC-721 token 获得持久、可转移身份。

### Verifiable Reputation

交互后的反馈上链，形成可审计 track record。

### Trust Without Intermediaries

通过加密签名、链上声誉、验证机制减少对中心平台的信任依赖。

### Economic Interoperability

Agent 可以 autonomously discover、verify、pay each other，和 x402 形成组合：

- ERC-8004 解决“我应该相信哪个 agent / service”。
- x402 解决“我如何按次支付这个 agent / service”。

---

## 3. 三个核心组件

### 3.1 Identity Registry

每个 agent mint 一个 ERC-721 token。

- token ID = agent 的唯一 identifier。
- token URI 指向 agent card。

Agent card 应包含：

- name and description。
- API endpoints，例如 A2A Protocol、MCP、HTTP。
- supported trust models。
- DID / ENS identifiers。
- agent wallet address for payments，如果有。

学习重点：Identity Registry 不是单纯 NFT，而是 agent discovery 的身份入口。

### 3.2 Reputation Registry

客户端和 agent 交互后，可以提交结构化 feedback 到链上。

Feedback 包括：

- values：衡量 uptime、success rate、quality 等属性。
- tags：例如 `fast`、`accurate`、`DeFi`。
- optional `feedbackURI`：详细 off-chain review。
- content hash：保证 off-chain 内容完整性。

文档强调：feedback 是 permanent and immutable。

### 3.3 Validation Registry

状态：coming soon。

用途：高价值任务中，由第三方 validators 验证 agent work。

验证模型不绑定具体实现，可支持：

- TEE。
- zkML。
- fraud proofs。
- 其他 cryptographic / third-party validation models。

---

## 4. Interaction Flow

官方流程：

1. Service / Agent A registers identity。
2. Client / Agent B discovers agents。
3. Client checks reputation。
4. Client sends service request + x402 payment。
5. Service returns response。
6. Client submits feedback to registries。

这条链路很适合本学习计划的 agentic payments 项目：

```text
ERC-8004 agent identity + reputation
        ↓
agent discovery / trust decision
        ↓
x402 paid request
        ↓
service result
        ↓
feedback back to ERC-8004 reputation registry
```

---

## 5. Use Cases

### Agentic Services Marketplace

- Oracles：price feeds、weather、sports scores。
- Market ratings & analytics：risk assessment、credit scoring、sentiment analysis。
- APIs as agents：weather、translation、image processing 等 API 都可以注册成 agent。
- Reputation-gated access：服务可按调用方链上声誉过滤或限制访问。

### Agent Routing Systems

Routing agent 根据以下维度选择服务提供者：

- Latency。
- Price。
- Reputation。
- Specialization。

### AI Agent Marketplaces

- Agents register services with pricing。
- Clients discover agents via reputation。
- Automated service discovery and payment。

### Autonomous Service Networks

- Agents hire other agents for subtasks。
- Reputation-based trust decisions。
- Automatic feedback loops。

### DeFi Agent Protocols

- Portfolio management agents。
- Trading strategy agents。
- Yield optimization agents。

### Enterprise Agent Ecosystems

- Internal agent directories。
- Cross-organization agent collaboration。
- Compliance and audit trails。

---

## 6. Best Practices

### Registration

- 使用描述清晰的 agent name。
- 文档要充分说明能力边界。
- 提供多种 endpoint types，提高集成灵活性。
- 随能力变化更新 agent cards。
- 使用 ENS names 方便发现。

### Reputation Management

- 每次 interaction 后提交 honest feedback。
- 使用 consistent tag taxonomies。
- 重要交互附带 detailed reviews。
- 对自己 agents 的 feedback 做响应或运营维护。

### Security

- 支付前 verify agent signatures。
- 高价值交易前 check reputation。
- critical operations 使用 validation registry。
- 持续 monitor feedback。

---

## 7. Advanced Features

### Cross-Chain Agent Discovery

思路：从其他链查询 agent card，在 Monad 上注册 mirror，并关联 reputation data。

### Reputation Aggregation

可构建自定义 trust score。

官方示例思路：

- recent feedback 权重 0.7。
- historical feedback 权重 0.3。
- recent 取最近 10 条。

### Validation Integration

未来可接入 TEE-based validation：

- submit to validation registry。
- TEE verifies execution。
- on-chain proof recorded。

---

## 8. Contract Addresses

官方文档给出 Monad 上 ERC-8004 地址：

| Contract | Address | 验证 |
|---|---|---|
| Identity Registry | `0x8004A169FB4a3325136EB29fA0ceB6D2e539a432` | 已用 `eth_getCode` 在 `https://rpc.monad.xyz` 验证有 code |
| Reputation Registry | `0x8004BAa17C55a88189AE136b182e5fdA19dE9b63` | 已用 `eth_getCode` 在 `https://rpc.monad.xyz` 验证有 code |
| Validation Registry | coming soon | 暂无地址 |

验证输出摘要：

```text
Identity Registry code_len 262 has_code True
Reputation Registry code_len 262 has_code True
```

注意：任何后续部署、调用、教学材料中引用地址前，仍应回查官方文档或链上 code，避免地址过期或网络混淆。

---

## 9. 与 x402 的组合关系

ERC-8004 和 x402 是 Monad agentic commerce 的两个互补模块：

- ERC-8004：身份、发现、声誉、验证。
- x402：HTTP paid endpoint、微支付、按次/API/agent service 付费。

推荐 demo 组合：

1. 注册一个 API agent 的 identity。
2. agent card 写入 HTTP 或 MCP endpoint、服务描述、价格说明、支付钱包地址。
3. client 读取 identity + reputation。
4. client 用 x402 向该 endpoint 发起付费请求。
5. 服务返回结果。
6. client 向 Reputation Registry 提交反馈。

---

## 10. 学习计划中的实验设计

### 入门实验：理解 ERC-8004 的三层模型

目标：能解释 Identity / Reputation / Validation 的分工。

任务：

1. 阅读官方 ERC-8004 guide。
2. 绘制 agent interaction flow。
3. 写一个 agent card JSON 草案。
4. 标注 endpoint、payment wallet、trust model、description。

验收：

- 能说明 ERC-721 token ID 与 agent identity 的关系。
- 能说明 feedbackURI 与 content hash 的作用。
- 能说明 Validation Registry 为什么适合 high-stakes tasks。

### 进阶实验：Agent discovery + x402 payment

目标：把 ERC-8004 与 x402 串起来。

任务：

1. 使用本项目 x402 paid endpoint。
2. 为该 endpoint 设计 agent card。
3. 读取 Identity Registry / Reputation Registry 地址。
4. 模拟 client 根据 reputation 选择 agent。
5. 用 x402 完成 paid request。
6. 生成一条 feedback JSON。

验收：

- 能讲清楚 discover → check reputation → x402 pay → submit feedback 的闭环。
- 能说明 reputation-gated access 和 agent routing 的价值。

### 高阶实验：Agent marketplace / routing prototype

目标：做一个最小 agent routing system。

任务：

1. 准备 3 个 mock agents：weather、translation、market-analysis。
2. 为每个 agent 设计 agent card。
3. 为每个 agent 设计 reputation score。
4. routing agent 根据 latency / price / reputation / specialization 选择服务。
5. 选中后通过 x402 paid endpoint 调用。
6. 调用结束生成 feedback。

验收：

- 有清晰 agent routing 决策日志。
- 有 x402 paid endpoint 调用记录。
- 有 feedback 结构化输出。

---

## 11. 后续使用规则

1. Monad agentic payments 模块中，ERC-8004 负责 trust layer，x402 负责 payment layer。
2. 不把 ERC-8004 简化成 NFT；它的重点是 agent identity + reputation + validation。
3. Validation Registry 目前按 coming soon 处理，不能假装已有完整地址或功能。
4. 合约地址使用前必须再次从官方文档或链上 `eth_getCode` 验证。
5. 所有 agent card 都要包含 endpoint、能力描述、trust model、payment wallet、可选 DID/ENS。
6. Reputation feedback 要设计 tag taxonomy，避免随意打标签导致不可聚合。
7. 高价值任务前必须先 check reputation，再 payment。
