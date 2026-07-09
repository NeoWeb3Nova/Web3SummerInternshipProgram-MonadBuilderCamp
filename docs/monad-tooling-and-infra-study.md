# Monad Tooling & Infrastructure 学习笔记

## 来源

- 官方文档：<https://docs.monad.xyz/tooling-and-infra>
- 本地源码快照：`docs/monad-tooling-and-infra-source.md`
- 快照来源：`monad-llms-full.txt` 中 Tooling and Infrastructure 相关章节
- 快照体量：274,019 chars / 5,868 lines
- SHA256：`93cebc74ba09ad327da733fb6229204c36146222af30bd92a89cda0f2151a6bf`

---

## 0. 核心原则：不要从零开始造工具与基础设施

这份文档在学习计划中的作用不是“背 provider 名单”，而是建立工程判断：

> 在 Monad 上做项目时，先查现成 tooling / infra，再决定是否需要自研。

默认决策顺序：

1. 先查 Monad 官方 Tooling & Infrastructure。
2. 找到支持 Mainnet / Testnet 的成熟 provider。
3. 用官方文档、provider docs、实际 API/RPC/SDK 验证可用性。
4. 只有当现有工具不能满足核心差异化需求时，才考虑自研。

反模式：

- 自己写 block explorer。
- 自己从 RPC 轮询所有 logs 做长期 indexer。
- 自己造 bridge。
- 自己造 oracle。
- 自己造 onramp/offramp。
- 自己造 wallet infra。
- 自己造完整 analytics pipeline。
- 自己造 x402 facilitator。

正确方式：用现成基础设施把产品闭环跑通，把时间投入到业务逻辑、用户体验和 Monad 特性上。

---

## 1. 文档覆盖的大类

官方 Tooling & Infrastructure 覆盖：

- Agentic Payments
- Analytics
- Block Explorers
- Cross-Chain
- Custody
- Common Data
- Indexers / Indexing Frameworks
- Onramps
- Oracles
- Payment Orchestrators
- RPC Providers
- Toolkits
- Monad Foundry
- Monad Solonet
- Account Abstraction Providers
- Embedded Wallets
- Wallet Infrastructure
- Smart Account Implementations
- Hardware Wallets
- Institutional Wallets
- Multisig Wallets
- Software Wallets

---

## 2. Provider 总览

### Agentic Payments

- Monad x402 Facilitator
- MPP SDK

使用规则：

- HTTP paid endpoint / agentic payments 优先看 x402 guide 和 Monad x402 Facilitator。
- Machine Payments Protocol 相关集成看 `@monad-crypto/mpp`。

### Analytics

- Birdeye
- Blockaid
- Bubblemaps
- CoinGecko
- Collab.Land
- DeBank
- DeFiLlama
- Dune
- Flipside
- InsightX
- Matrica
- Nansen
- Phalcon
- Philidor
- Tenderly

使用规则：

- Dashboard、市场数据、用户行为、风险分析，不要先自建数据仓库。
- DeFi TVL/协议数据先看 DeFiLlama。
- 钱包画像/聪明钱/链上洞察先看 Nansen、DeBank。
- 调试和模拟先看 Tenderly、Phalcon。

### Block Explorers

- BlockVision
- Monadscan

使用规则：

- 交易、地址、合约、浏览器链接优先用官方列出的 explorer。
- UserOp 和 detailed transaction explorer 需求先查文档支持状态。

### Cross-Chain

- Axelar
- Bungee Exchange
- ChangeHero
- Chainlink CCIP
- Circle CCTP
- deBridge
- Flashnet
- Garden
- Gas.zip
- Houdini
- Hyperlane
- LayerZero
- Li.fi
- Particle Network
- Mayan
- Polymer
- Relay
- SimpleSwap
- Socket
- Squid
- Stargate
- Trails
- Trustware
- Wormhole

使用规则：

- 跨链消息、桥、聚合路由优先用成熟 cross-chain provider。
- USDC 相关优先考虑 Circle CCTP。
- 通用桥和跨链路由先查 Li.fi、Socket、Squid、Relay、Bungee 等。
- 不要为 hackathon / MVP 自造 bridge。

### Custody

- Anchorage Digital
- BitGo
- Coinbase Custody
- Fireblocks
- HexTrust

使用规则：

- 机构托管、合规钱包、企业资金管理先查 custody provider。
- 不要自己承担机构级私钥管理和合规托管。

### Common Data

- Allium
- Birdeye Data Services
- Codex
- Dune Sim
- GoldRush by Covalent
- Goldsky
- Mobula
- Moralis
- Quicknode
- Rarible
- Sequence
- SQD
- SonarX
- thirdweb
- Unmarshal
- Zerion

使用规则：

- NFT、token、portfolio、metadata、历史数据、价格数据、交易模拟，先查 common data providers。
- 如果只是展示资产、余额、NFT、activity feed，不要直接从 RPC 拼全套数据层。

### Indexing Frameworks

- Envio
- Ghost
- Goldsky
- Ormi
- Sentio
- SQD
- Streamingfast
- SubQuery
- The Graph

使用规则：

- 历史事件、leaderboard、activity feed、analytics dashboard 不要反复 `eth_getLogs`。
- MVP 可从 Envio / Goldsky / Ghost / SQD / SubQuery / The Graph 中选。
- 需要实时或复杂 pipeline 时再看 Streamingfast、Sentio 等。

### Onramps

- AgoraCrypto / AhoraCrypto
- Alchemy Pay
- alfred
- Banxa
- Blink
- Brale
- Bridge
- BTC Direct
- Capa
- Chainrails
- Coinbase Onramp & Offramp
- Coindisco
- Coinflow
- Daimo
- El Dorado
- FinchPay
- Flashnet
- Fonbnk
- Fun.xyz
- Guardarian
- Halliday
- HoneyCoin
- Koywe
- Meld
- Mercuryo
- MoonPay
- Onramp Money
- Onramper
- OSL Pay
- Paj
- Peer
- Ramp Network
- Rampnow
- Suby
- Swapped
- Swapper Finance
- Switch
- Transak
- Unlimit
- UR
- Walapay
- zerohash

使用规则：

- 法币入金、出金、卡支付、地区合规覆盖，先查 onramp provider。
- 不要自己处理支付牌照、KYC、法币通道。

### Oracles

- Chainlink
- Chronicle
- Pyth
- Redstone
- Stork
- Supra
- Switchboard

使用规则：

- 价格、随机数、外部数据优先用 oracle provider。
- DeFi 项目不要自写中心化价格喂价，除非明确是实验。

### Payment Orchestrators

- Brale
- Bridge
- Checker
- zerohash

使用规则：

- 稳定币发行、支付流、结算编排、合规支付路径优先查 payment orchestrators。

### RPC Providers

- Alchemy
- Ankr
- Blockdaemon
- BlockPI
- Chainstack
- dRPC NodeCloud
- Dwellir
- Envio
- GetBlock
- OnFinality
- Quicknode
- Spectrum
- Tatum
- thirdweb
- Triton One
- Validation Cloud

使用规则：

- 不要默认只用一个公共 RPC 上生产。
- 前端、后端、indexer、script 要区分 RPC 需求：rate limit、batch limit、archive/historical state、debug/trace、WebSocket。
- 生产环境至少准备 provider fallback。

### Toolkits

- Hardhat
- Monad Foundry
- Monad Solonet

使用规则：

- 合约开发优先 Hardhat / Foundry。
- Monad 专有 EVM 行为、staking precompile、Monad EVM execution 相关优先看 Monad Foundry。
- 本地实验链看 Monad Solonet。

### Account Abstraction Providers

- Alchemy
- Biconomy
- FastLane
- Gelato
- Openfort
- Pimlico
- Sequence
- thirdweb
- Zerodev

使用规则：

- sponsored tx、bundler、paymaster、smart account，不要从零实现 AA stack。
- 先选 provider，再做产品 UX。

### Embedded Wallets

- Alchemy
- Coinbase Developer Platform
- Crossmint
- Cubist
- Dynamic
- Fordefi
- MetaMask Embedded Wallet
- Para
- Phantom
- Portal
- Privy
- Reown
- Sequence
- thirdweb
- Turnkey

使用规则：

- 邮箱、社交登录、passkey、MPC、嵌入式钱包优先用 embedded wallet provider。
- 学习计划中如需新手低门槛登录，优先 Para / Privy / Dynamic / Reown / thirdweb 等，而不是自己做密钥托管。

### Wallet Infrastructure / Smart Accounts

- Biconomy
- MetaMask Smart Accounts Kit
- Pimlico
- Zerodev

使用规则：

- Smart account implementation、paymaster、session keys、gas sponsorship，先查这些现成方案。

### Wallets

Hardware:

- D'Cent Wallet
- Ledger
- Safepal
- Tangem

Institutional:

- Cubist
- Porto by Anchorage Digital
- Utila

Multisig:

- Safe Wallet

Software:

- Ambire
- Backpack
- Binance Wallet
- Bitget Wallet
- Coin98
- Exodus
- HaHa
- imToken
- Keplr
- MetaMask
- OKX
- Rabby
- Safepal
- Trust Wallet
- Uniswap Wallet
- Zerion

使用规则：

- 用户钱包连接前，先确认目标钱包是否支持 Monad mainnet/testnet。
- 多签优先 Safe。
- 不要假设 Ledger 等硬件钱包已经支持，必须回查官方表。

---

## 3. 按产品需求选工具

### 做 x402 / agentic payments

优先：

1. Monad x402 Facilitator。
2. x402 guide。
3. MPP SDK。
4. ERC-8004 做 identity / reputation。

不要：自己造 facilitator、自己造 agent payment protocol。

### 做 Agent marketplace / Trustless Agents

优先：

1. ERC-8004 Identity / Reputation Registry。
2. x402 Facilitator。
3. Common Data 或 Indexer 做 agent activity feed。
4. Wallet infra / embedded wallet 降低用户门槛。

不要：自己造身份注册表和声誉系统，除非只是 mock demo。

### 做 DeFi / Trading / Portfolio

优先：

1. Oracles：Chainlink / Pyth / Redstone / Chronicle 等。
2. Common Data：Moralis / GoldRush / Birdeye / DeBank / Zerion 等。
3. Analytics：Dune / Nansen / DeFiLlama / Tenderly 等。
4. RPC fallback。
5. Indexer。

不要：自己从零聚合所有 token、price、wallet、history 数据。

### 做 Activity feed / Leaderboard / Analytics Dashboard

优先：

1. Envio / Goldsky / Ghost / SQD / SubQuery / The Graph。
2. Common Data provider。
3. Dune / Flipside。

不要：前端循环 `eth_getLogs`。

### 做 Wallet onboarding

优先：

1. Reown / Privy / Para / Dynamic / thirdweb / Coinbase Developer Platform。
2. Account abstraction provider。
3. Smart account implementation。

不要：自己托管私钥、自己实现社交登录钱包。

### 做 Cross-chain / Bridge

优先：

1. Circle CCTP for USDC。
2. LayerZero / Hyperlane / Wormhole / Axelar / Chainlink CCIP。
3. Li.fi / Socket / Squid / Relay / Bungee for aggregation/routing。

不要：hackathon 自造桥。

### 做 Onramp / Fiat payment

优先：

1. MoonPay / Transak / Coinbase Onramp / Ramp Network / Banxa 等。
2. 地区、KYC、费用、支持资产逐项核对。

不要：自己接法币支付和合规。

---

## 4. 项目开始前的基础设施检查清单

每个 Monad 项目开始前先回答：

1. 需要 RPC 吗？需要 public、dedicated、archive、debug/trace、WebSocket、batch 吗？
2. 需要历史数据吗？如果需要，选 indexer 或 common data provider。
3. 需要价格/外部数据吗？如果需要，选 oracle。
4. 需要钱包登录吗？如果需要，选 embedded wallet 或 Reown/AppKit 类方案。
5. 需要 gas sponsorship / smart accounts 吗？如果需要，选 AA provider。
6. 需要跨链资产或消息吗？如果需要，选 bridge / cross-chain provider。
7. 需要法币入口吗？如果需要，选 onramp。
8. 需要付费 API / agent payment 吗？如果需要，选 x402 / MPP。
9. 需要 agent identity / reputation 吗？如果需要，选 ERC-8004。
10. 需要 analytics / risk / monitoring 吗？如果需要，选 analytics provider。

---

## 5. 学习计划中的任务设计

### 入门任务：工具地图

目标：知道 Monad 已有哪些现成工具。

任务：

1. 选一个产品想法。
2. 按上面的 10 个问题列出所需 infra。
3. 从官方 Tooling & Infrastructure 文档中选择 provider。
4. 写出“为什么不用自研”。

验收：

- 输出一张项目 infra map。
- 每个模块至少有一个官方文档中的 provider 备选。

### 进阶任务：MVP infra selection

目标：给 x402 + ERC-8004 agentic commerce demo 选型。

推荐组合：

- Payment：Monad x402 Facilitator。
- Trust：ERC-8004 Identity / Reputation Registry。
- Wallet：Privy / Para / Reown / thirdweb 任选其一。
- RPC：Alchemy / Quicknode / Ankr / thirdweb 等任选，保留 fallback。
- Indexer：Envio / Goldsky / Ghost。
- Explorer：Monadscan / BlockVision。
- Analytics：Dune / Tenderly / DeFiLlama / Nansen 等按需求选。

验收：

- 写出每个 provider 的用途。
- 写出不用 provider 会增加的工程成本。
- 写出最小可替换方案。

### 高阶任务：Build vs Buy 决策

目标：训练工程决策，而不是盲目堆技术。

输出格式：

| 模块 | 现成工具 | 自研成本 | 风险 | 选择 |
|---|---|---|---|---|
| RPC | Alchemy / Quicknode / Ankr | 高 | rate limit / reliability | buy |
| Indexer | Envio / Goldsky | 中高 | 数据一致性 / reorg / 历史同步 | buy |
| Agent payment | x402 Facilitator | 高 | settlement / gas / security | buy |
| Core product logic | 自研 | 必须 | 产品差异化 | build |

---

## 6. 后续使用规则

1. 以后做 Monad 项目，先查 `docs/monad-tooling-and-infra-source.md` 和官方在线文档。
2. 不为 MVP 自研基础设施，除非它就是项目核心卖点。
3. 引用 provider 支持状态前必须回查官方表，因为 Mainnet/Testnet 支持会变化。
4. 生产项目不要单 RPC、单 indexer、单外部服务无 fallback。
5. 学习计划中每个项目都要写 infra map，强制说明哪些 buy、哪些 build。
6. x402 + ERC-8004 主线中，优先用已有 x402 facilitator、ERC-8004 registry、indexer、wallet provider，产品重点放在 agent 发现、选择、支付、反馈闭环。
