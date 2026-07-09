# Monad x402 技术文档学习笔记

## 来源

- 官方文档：<https://docs.monad.xyz/guides/x402>
- 本地源码快照：`docs/monad-x402-guide-source.md`
- 快照体量：35,220 chars / 220 lines
- SHA256：`e071e136abac4c608d79aaa52440bc8f5a40eadc8a3afca4b6c270b3b021ac8c`
- Facilitator URL：`https://x402-facilitator.molandak.org`
- 已实测 `GET /supported` 可访问，返回支持 Mainnet / Testnet 的 exact 与 upto scheme。

---

## 1. x402 是什么

x402 是把 HTTP `402 Payment Required` 重新作为互联网原生微支付协议使用。

核心流程：

1. Client 请求某个资源。
2. Server 返回 `402`，附带 JSON payment requirement。
3. Client 签署支付授权后重新请求。
4. Server 验证支付，成功后返回内容。

它解决的不是“钱包转账”本身，而是“HTTP API / 内容 / 计算资源如何按次收费”的问题。

适合场景：

- API 按次计费。
- 内容解锁。
- AI agent 调用付费工具。
- 机器对机器支付。
- LLM token / bandwidth / compute 等按量计费。

---

## 2. 为什么 x402 适合 Monad

官方文档给出的 Monad 适配理由：

- 10,000 TPS。
- 约 0.4 秒 block time。
- single-slot finality。
- parallel execution。
- 极低费用。

结论：Monad 的低延迟、低成本和高吞吐使它适合真正的 micropayments 和 agent-to-agent commerce。大量 AI agents 按 API call 支付时，Monad 可以降低链上结算成本和拥堵风险。

---

## 3. 两种支付流

### 3.1 Direct Payment

Resource server 自己处理验证和结算。

特点：

- 架构更直接。
- 服务端需要承担更多链上逻辑。
- 更适合教学、实验、极简 demo。

### 3.2 Facilitator Flow（生产推荐）

官方推荐生产环境使用 facilitator。

Facilitator 可以：

- batch transactions。
- cover gas。
- handle refunds。
- simplify client logic。
- 提供 `/supported`、`/verify`、`/settle` API。

Monad 官方 guide 使用的 facilitator：

```text
https://x402-facilitator.molandak.org
```

---

## 4. Monad x402 的基础参数

### Testnet

```ts
const MONAD_NETWORK = "eip155:10143";
const MONAD_USDC_TESTNET = "0x534b2f3A21130d7a60830c2Df862319e593943A3";
const FACILITATOR_URL = "https://x402-facilitator.molandak.org";
```

### Mainnet

Facilitator `GET /supported` 实测支持：

```text
eip155:143
```

### Facilitator signer

实测 `/supported` 返回：

```text
0x7f6a2850669202519f0FE8aa912451238820Db86
```

### x402 version

Monad Facilitator only supports x402 version 2 and above。

迁移参考：

```text
https://docs.x402.org/guides/migration-v1-to-v2
```

---

## 5. 支持的 payment schemes

官方文档列出 Monad facilitator 支持两个 x402 v2 schemes。

| Scheme | 适合场景 | 机制 |
|---|---|---|
| `v2-eip155-exact` / `exact` | 固定价格支付，USDC 默认推荐 | EIP-3009 `transferWithAuthorization`，或非 EIP-3009 token 用 Permit2 proxy fallback |
| `v2-eip155-upto` / `upto` | 变量金额、按量计费，例如 LLM tokens、带宽、计算 | Permit2-only，client 签最大额度，facilitator 按实际使用量结算，支持 $0 settlement |

学习重点：

- USDC on Monad 推荐使用 `exact`。
- `upto` 适合 usage-based billing。
- `upto` 依赖 canonical `x402UptoPermit2Proxy`：

```text
0x4020A4f3b7b90ccA423B9fabCc0CE57C6C240002
```

- 使用 `upto` 时，`@x402/evm` 要用 `2.12.0` 或确认更新版本仍引用正确 proxy 地址。
- `@x402/evm` 2.9.0–2.11.0 会引用未部署在 Monad 的 proxy 地址：

```text
0x402039b3d6E6BEC5A02c2C9fd937ac17A6940002
```

该版本坑会导致 settlement 失败且错误不清晰。

---

## 6. Next.js 集成主线

官方 guide 的 app 形态：Next.js + TypeScript + Tailwind + App Router。

安装依赖：

```bash
npm install @x402/core @x402/evm @x402/fetch @x402/next
```

环境变量：

```env
PAY_TO_ADDRESS=0xYourWallet
```

`payTo` 是收款地址，也是后端配置 payment requirement 的核心字段。

---

## 7. 服务端 payable endpoint 心智模型

示例文件：

```text
src/app/api/premium/route.ts
```

服务端需要做：

1. 配置 Monad network：`eip155:10143`。
2. 配置 Monad USDC testnet token。
3. 配置 facilitator client。
4. 创建 `x402ResourceServer`。
5. 创建 `ExactEvmScheme`。
6. 注册自定义 money parser，把 `$0.001` 转成 USDC 6 decimals 的最小单位。
7. `server.register(MONAD_NETWORK, monadScheme)`。
8. 设置 route config：
   - `scheme: "exact"`
   - `network: MONAD_NETWORK`
   - `payTo: PAY_TO`
   - `price: "$0.001"`
   - `resource: "http://localhost:3000/api/premium"`
9. 用 `withX402(handler, routeConfig, server)` 包装 GET handler。

关键点：USDC 是 6 decimals，`0.001 USDC = 1000` atomic units。

---

## 8. 客户端消费 payable endpoint 心智模型

客户端需要：

1. 连接钱包，拿到 `address` 和 `walletClient`。
2. 构造 x402-compatible EVM signer，核心能力是 `signTypedData`。
3. 创建 `ExactEvmScheme(evmSigner)`。
4. 创建 `x402Client().register("eip155:10143", exactScheme)`。
5. 用 `wrapFetchWithPayment(fetch, client)` 包装 fetch。
6. 请求 `/api/premium`。
7. 如果收到 402，x402 client 会处理签名支付再重试。
8. 成功后拿到 premium content。

需要做好的 UX：

- 钱包未连接。
- 用户拒签。
- USDC 余额不足。
- facilitator unexpected error。
- 402 payment-required header 解析失败。

---

## 9. Facilitator API

### `GET /supported`

返回支持的 networks、schemes、signers。

本地实测返回摘要：

```json
{
  "kinds": [
    { "network": "eip155:143", "scheme": "upto", "x402Version": 2 },
    { "network": "eip155:143", "scheme": "exact", "x402Version": 2 },
    { "network": "eip155:10143", "scheme": "exact", "x402Version": 2 },
    { "network": "eip155:10143", "scheme": "upto", "x402Version": 2 }
  ],
  "signers": {
    "eip155:10143": ["0x7f6a2850669202519f0FE8aa912451238820Db86"],
    "eip155:143": ["0x7f6a2850669202519f0FE8aa912451238820Db86"]
  }
}
```

### `POST /verify`

验证 payment signature。

核心数据结构：

- `x402Version: 2`
- `payload.authorization`
- `payload.signature`
- `accepted.scheme`
- `accepted.network`
- `accepted.amount`
- `accepted.asset`
- `accepted.payTo`
- `accepted.maxTimeoutSeconds`
- `accepted.extra.name = "USDC"`
- `accepted.extra.version = "2"`

`exact` + USDC 使用 EIP-3009 `TransferWithAuthorization` typed data。

### `POST /settle`

执行链上支付，facilitator pays gas。

返回成功时会有 transaction；失败时看 `errorReason`。

---

## 10. 重要错误码

除普通 `200 / 4xx / 5xx` 外，官方特别提到：

```text
412 PRECONDITION_FAILED
```

含义：Permit2 payment 无法继续，因为用户对 proxy contract 的 Permit2 allowance 不足。

错误原因：

```text
PERMIT2_ALLOWANCE_REQUIRED
```

处理方式：client 需要 approve proxy via Permit2 后重试。

注意：这和 resource server 返回的 `402 Payment Required` 不是一回事。

---

## 11. 学习计划中的实验设计

### 入门实验

目标：理解 x402 不是普通转账，而是 HTTP paid endpoint。

任务：

1. 建立 Next.js app。
2. 创建 `/api/premium`。
3. 设置 `PAY_TO_ADDRESS`。
4. 用 testnet USDC 设置 `$0.001` 价格。
5. 前端点击 Pay & Unlock Content。
6. 钱包签名后解锁内容。

验收：

- 未支付访问会触发 402。
- 支付后返回 premium content。
- 能解释 `PAY_TO_ADDRESS`、`MONAD_NETWORK`、`MONAD_USDC_TESTNET`、`FACILITATOR_URL` 的作用。

### 进阶实验

目标：理解 agentic payments。

任务：

1. 写一个 Node.js agent script。
2. agent 自动请求 paid endpoint。
3. 收到 402 后自动签名并支付。
4. 获取内容后写入本地 JSON 或 Markdown。

验收：

- 无浏览器 UI 也能完成 paid API call。
- 能解释为什么 x402 适合 AI agent 调用付费工具。

### 高阶实验

目标：理解 exact vs upto。

任务：

1. 固定价格内容使用 `exact`。
2. 模拟 LLM token usage / bandwidth 使用 `upto`。
3. 处理 `412 PRECONDITION_FAILED` 和 Permit2 allowance。

验收：

- 能解释 `exact` 和 `upto` 的机制差异。
- 能说明为什么 `@x402/evm 2.12.0` 对 Monad upto 很重要。

---

## 12. 后续使用规则

1. 任何 Monad x402 demo 默认以 `x402 version 2+` 为基线。
2. Testnet 默认使用 `eip155:10143` 与 `0x534b2f3A21130d7a60830c2Df862319e593943A3`。
3. Mainnet 或 token 地址变更必须回查官方文档和 facilitator `/supported`。
4. 固定价格优先 `exact`；按量计费才考虑 `upto`。
5. 使用 `upto` 前先确认 Permit2 proxy 地址和 `@x402/evm` 版本。
6. UI 任务必须处理用户拒签、余额不足、facilitator error、Permit2 allowance required。
7. Agent 任务重点验证机器自动支付和访问 paid API 的闭环。
