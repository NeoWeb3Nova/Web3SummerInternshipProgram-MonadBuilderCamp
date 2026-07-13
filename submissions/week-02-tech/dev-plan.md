# Week 2 Day 2｜AI-assisted Dev Plan — Dev Builder

> 学员：Neo  
> 方向：Dev Builder（Tech）  
> 日期：2026-07-14  
> 今日任务：任务 15｜定义一个最小 Web3 原型，说明用户动作、技术组件、要读的文档、真实实现 / mock / 本周不做的边界。

---

## 1. 项目一句话

**MonadTally**：一个部署在 Monad 测试网上的链上计数器，带最小前端页面，支持钱包连接、读取计数、+1 写入、重置（仅 owner），并记录真实交易哈希。

> 选择计数器而非更复杂的 Escrow/Agent Wallet，是因为它是 Monad 测试网环境验证的最小闭环，且为 Week 3 组队保留可扩展接口。

---

## 2. 用户动作

| 用户动作 | 前端界面 | 链上结果 |
|---------|---------|---------|
| 连接钱包 | 点击 "Connect Wallet" | 获取用户地址，显示余额/网络 |
| 查看计数 | 页面自动读取 | 显示 `Counter.sol` 的 `number()` 值 |
| 增加计数 | 点击 "+1" 按钮 | 调用 `increment()`，生成 tx hash |
| 重置计数 | Owner 点击 "Reset" | 调用 `setNumber(uint256)`，仅 owner 可执行 |
| 查看交易 | 点击 tx hash 链接 | 跳转 Monad 测试网浏览器 |

---

## 3. 技术架构

```
┌─────────────────────────────────────┐
│          Frontend (Next.js)         │
│  React + Tailwind + viem + RainbowKit│
└──────────────┬──────────────────────┘
               │
┌──────────────▼──────────────────────┐
│         Wallet (MetaMask/Rabby)     │
│     Sign tx for Monad Testnet       │
└──────────────┬──────────────────────┘
               │
┌──────────────▼──────────────────────┐
│      Monad Testnet (EVM-compatible) │
│      Counter.sol (Solidity 0.8.x)   │
└─────────────────────────────────────┘
```

---

## 4. 技术组件清单

| 层级 | 组件 | 选择理由 | 是否本周实现 |
|------|------|---------|------------|
| 合约 | `Counter.sol` | 最小可运行状态合约，含 owner 权限 | ✅ 真实实现 |
| 合约测试 | Foundry test | 验证 owner 权限、increment/setNumber 逻辑 | ✅ 真实实现 |
| 部署脚本 | Foundry script (`Counter.s.sol`) | 一键部署到 Monad testnet | ✅ 真实实现 |
| 前端框架 | Next.js 14 (App Router) | 与 Week 3 组队栈一致 | ✅ 真实实现 |
| 钱包连接 | RainbowKit + wagmi | 降低钱包适配成本 | ✅ 真实实现 |
| 链交互 | viem | ESM-native，类型安全，配合 wagmi | ✅ 真实实现 |
| UI 样式 | Tailwind CSS | 快速、轻量、无需设计系统 | ✅ 真实实现 |
| 网络配置 | Monad Testnet RPC | 使用官方或社区 RPC | ✅ 真实实现 |
| 水龙头 | Monad Faucet | 获取测试 MON 用于部署/交易 | ✅ 真实实现 |
| 多链支持 | Sepolia fallback | 若 Monad 测试网不可用，先用 Sepolia 验证 | 🟡 可选 fallback |
| CI/CD | Vercel deploy | 部署前端页面，生成可访问链接 | 🟡 本周尽量做 |
| 复杂权限 | Role-based access control | 超出最小 Demo 范围 | ❌ 本周不做 |
| 后端服务 | Node/FastAPI API | 不需要读取任何链下状态 | ❌ 本周不做 |
| 多合约交互 | Factory / Proxy pattern | 超出本周 scope | ❌ 本周不做 |

---

## 5. 要读的文档（按优先级）

| 优先级 | 文档 | 用途 |
|-------|------|------|
| P0 | [Monad Developer Docs](https://docs.monad.xyz/) | RPC、Faucet、网络信息 |
| P0 | [Foundry Book](https://book.getfoundry.sh/) | 编译、测试、部署脚本 |
| P0 | [viem docs](https://viem.sh/) | 合约读取/写入、交易构造 |
| P0 | [wagmi + RainbowKit docs](https://www.rainbowkit.com/docs) | 钱包连接配置 |
| P1 | [Solidity 0.8.x docs](https://docs.soliditylang.org/) | owner 权限、事件定义 |
| P1 | [Next.js App Router](https://nextjs.org/docs) | 前端路由与客户端组件边界 |
| P2 | [EIP-1193](https://eips.ethereum.org/EIPS/eip-1193) | 理解 Provider 接口（可选） |

---

## 6. 真实实现 / Mock / 本周不做

### 6.1 真实实现（必须跑通）

- [ ] `Counter.sol` 合约编写与本地 Foundry 测试通过
- [ ] 使用 Foundry script 部署到 Monad Testnet，记录真实 contract address + deploy tx hash
- [ ] 最小 Next.js 前端：连接钱包、读取计数、调用 `increment()`、显示 tx hash
- [ ] GitHub repo 提交，含 README（运行步骤、合约地址、截图）

### 6.2 Mock / Fallback

- 如果 Monad Faucet 暂时不可用：先用本地 Anvil 运行完整流程，再迁移到 Monad。
- 如果 RainbowKit 配置遇到 Monad 链不支持的问题：改用 viem 自定义 chain + 原生 MetaMask 调用。
- 如果 Vercel 部署失败：保留本地 `npm run dev` 录屏作为证明。

### 6.3 本周不做

- 不实现多用户权限、不计入复杂业务逻辑。
- 不接入真实支付、Agent Wallet、Escrow 等 Week 3 方向。
- 不做移动端适配、不做动画、不做 dark mode。
- 不做单元测试覆盖率报告、不做 CI pipeline。

---

## 7. AI 与人工分工

| 任务 | AI 负责 | 人类负责 |
|------|--------|---------|
| 合约代码 | 生成 `Counter.sol` 骨架 | review owner 逻辑、运行测试 |
| Foundry 脚本 | 生成部署脚本模板 | 配置私钥/环境变量、执行部署 |
| 前端代码 | 生成 RainbowKit + viem 调用组件 | 调整 UI、验证交易 |
| README | 生成结构 | 填入真实 contract address 和 tx hash |
| 部署决策 | 提供 RPC/Faucet 建议 | 最终选择网络、执行真实部署 |
| 私钥/助记词 | ❌ 绝不接触 | 独立管理 .env |

---

## 8. 验收标准

- [ ] `forge test` 本地通过。
- [ ] Monad Testnet 上存在已部署的 `Counter` 合约地址。
- [ ] 前端可连接钱包，点击 +1 后生成真实 tx hash 并在链上确认。
- [ ] README 包含：运行步骤、合约地址、部署 tx hash、前端截图/链接。
- [ ] AI Collaboration Log 更新 Day 2 协作记录。

---

## 9. 风险提示

| 风险 | 影响 | 应对 |
|------|------|------|
| Monad Testnet RPC 不稳定 | 部署/读取失败 | 切 Anvil 本地或 Sepolia fallback |
| Faucet 限额/不可用 | 无测试 MON | 本地 Anvil 验证，或申请社区 faucet |
| RainbowKit 不支持 Monad chain | 钱包连接报错 | 改用 viem custom chain + wagmi |
| 私钥误提交到 GitHub | 资金损失 | 使用 `.env` + `.gitignore`，AI 不接触私钥 |
| Scope 蔓延 | 做不完 Demo | 严格遵守「本周不做」清单 |

---

## 10. 下一步

1. Day 2 下午：初始化 Foundry 项目，写 `Counter.sol` + test。
2. Day 3：配置 Monad Testnet，完成首次部署。
3. Day 4：搭建 Next.js 前端，实现读取与写入。
4. Day 5：整理 README、截图/录屏、提交 Portfolio。
