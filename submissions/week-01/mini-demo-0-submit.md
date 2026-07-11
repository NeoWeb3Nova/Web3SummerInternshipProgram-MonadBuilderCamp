# Week 1｜Mini Demo 0 提交内容

---

## 1. Week 1 作品链接

GitHub Repo（Week 1 提交物目录）：
https://github.com/neo-web3/Web3SummerInternshipProgram-MonadBuilderCamp/tree/master/submissions/week-01/mini-demo-0.md

> 注：若 Repo 为私有或链接需调整，请替换为实际仓库地址。

---

## 2. Demo 说明文档 / 截图 / 链上记录

完整提交材料：`submissions/week-01/mini-demo-0.md`

核心链上证据：
- 钱包地址：`0x650cd30a58e6893169F41CaC9379D02e7E34653F`
- 合约部署交易：[`0x1b552a...a98ed`](https://testnet.monadscan.com/tx/0x1b552a774e6f33dc0dfbc03890ebaedd007e6a38d9557b5a3205a9f5943a98ed)
- 部署合约地址：[`0xb029...f0cba`](https://testnet.monadscan.com/address/0xb02956728ef9b72adb805a5507024216dd8f0cba)
- 测试网转入交易 1：[`0xa7604...9fac0`](https://testnet.monadscan.com/tx/0xa760432eb5576ef5b0b5be766279fba20675180ef4263bc48b01f260ddc9fac0)
- 测试网转入交易 2：[`0xb1616...0cd8b`](https://testnet.monadscan.com/tx/0xb161638f001a63a3fbdae200213690059f4b14fe88619e610146b0246530cd8b)

截图待补充：钱包网络配置 / Faucet 领取 / Explorer 交易详情（保存至 `assets/week-01/`）。

---

## 3. 方向选择

**Tech**

选择理由：
- Week 1 已完成 Monad Testnet 钱包配置、RPC 验证、测试网交易与智能合约部署。
- 已沉淀技术学习材料：网络配置、合约模板、x402 微支付、ERC-8004 Trustless Agents。
- 已有明确 Demo 方向：基于 Monad 高吞吐特性的链上任务/积分/徽章系统（Monad Quest Arena）。

---

## 4. 一句话作品集 / 简历说明

> 在 Monad Testnet 上完成钱包配置、RPC 验证、测试网交易与智能合约部署（部署合约 `0xb029...f0cba`），并围绕“高频链上任务与积分系统”输出技术-运营-研究三维度方案，为后续 DApp 开发留下可验证的 Proof of Work。

---

## 5. Week 2 继续推进的问题

1. 把 `QuestProof.sol` 或 `Gmonad.sol` 正式部署到 Monad Testnet，获得合约地址与交易哈希。
2. 用 Vite + React + wagmi/viem 做一个最小前端，实现连接钱包、显示余额、调用合约。
3. 验证 x402 在 Monad Testnet 上的支付流程，判断是否适合作为 Quest Arena 的奖励结算层。
4. 找 1-2 位同学试用最小 Demo，收集“哪里不懂、哪里卡住”的真实反馈。
5. 持续记录 AI 协作边界：AI 生成代码，人工审查、测试、部署和解释。

---

## 补充说明

- **真实链上操作**：合约部署 + 测试 MON 转入 + RPC `eth_chainId` 实测。
- **AI 辅助部分**：文档结构化、参数提取、合约模板生成、每日打卡草稿。
- **人工判断与修改**：安全边界（AI 不接触私钥/助记词）、官方文档优先、来源交叉验证、场景选择（Onchain Quest Arena）、方向选择 Tech。

> 未提交私钥、助记词、API Key、.env 文件或会议链接。
