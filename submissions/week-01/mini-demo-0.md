# Week 1｜Mini Demo 0 提交材料

> 提交日期：2026-07-11
> 项目：Web3 暑期实习计划 - Monad Builder Camp
> 学员：Neo

---

## 一、我做了什么

Week 1 的核心产出不是一段完整代码，而是一套“从 0 到链上”的可验证证据链：

| 产出 | 路径 | 说明 |
|------|------|------|
| 项目总览与导航 | `README.md` | 把 5 周计划、Track 选择、每日节奏、交付物标准整理成可浏览的项目入口。 |
| 开营仪式学习材料 | `docs/opening-ceremony.md` / `docs/opening-ceremony-transcript.md` | 从本地视频转录并整理出结构化纪要。 |
| DevRel 分享会材料 | `docs/devrel-growth.md` / `docs/devrel-growth-transcript.md` | 把 7 月 6 日分享会沉淀为学习笔记。 |
| Monad 技术笔记 | `docs/monad-technical-notes.md` | 基于 Box 分享整理 Monad 高吞吐、流水线共识、乐观并行执行、MonadDB 等核心概念。 |
| Monad Testnet 网络配置 | `submissions/week-01/network-config.md` | 记录 RPC、Chain ID、Explorer、Faucet，并用 `eth_chainId` 实测验证 `0x279f`。 |
| 钱包与测试网配置实验 | `experiments/monad-wallet-setup/README.md` | 记录钱包配置步骤、RPC 验证结果、安全边界。 |
| 第一笔链上交易记录 | `submissions/week-01/first-tx.md` | 交易完成前模板，交易完成后回填哈希与 Explorer 链接。 |
| 高频交互场景研究 | `submissions/week-01/monad-high-frequency-app.md` | 选择“Onchain Quest Arena”作为 Monad 高频交互场景，从 Research / Tech / Ops 三个维度拆解。 |
| x402 技术研究 | `docs/monad-x402-study.md` | 学习 Monad 官方 x402 微支付指南，记录 Testnet 参数、Facilitator、direct/facilitator 两种支付流。 |
| ERC-8004 技术研究 | `docs/monad-erc-8004-study.md` | 学习 Trustless Agents 标准，记录 Identity/Reputation/Validation Registry 和合约地址。 |
| 每日学习日志 | `daily/2026-07-07.md` / `2026-07-08.md` / `2026-07-09.md` | 记录每天任务、AI 协作、遇到的问题和复盘。 |

---

## 二、哪部分是真实链上操作

目前项目中**已确认的真实链上验证**是：

- 用 JSON-RPC 调用 `https://testnet-rpc.monad.xyz` 的 `eth_chainId`，实测返回 `0x279f`（十进制 10143）。
- 在 `docs/monad-erc-8004-study.md` 和 `docs/monad-x402-study.md` 中，使用 `eth_getCode` 或 Facilitator `/supported` 接口验证了 Monad 主网/测试网上的公开合约地址和配置。

**待你回填的真实链上操作**（请用公开信息替换下方占位符）：

| 字段 | 占位值 | 你的真实值 |
|------|--------|-----------|
| 钱包地址 | `0x...` | **待填写** |
| 交易类型 | 小额转账 / 合约部署 / 合约交互 | **待填写** |
| 交易哈希 | `0x...` | **待填写** |
| Explorer 链接 | https://testnet.monadvision.com/tx/0x... | **待填写** |
| Gas / Fee | 待记录 | **待填写** |
| 状态 | 待确认 | **待填写** |

> 安全提醒：只发公开地址和交易哈希，不要发私钥 / 助记词 / API Key。

---

## 三、哪部分由 AI 辅助完成

| 工作 | AI 辅助内容 | 人工判断/修改 |
|------|------------|--------------|
| 视频/音频转录 | 用 FunASR 从本地视频提取字幕并生成转录稿。 | 人工校对转录分段，补全发言人、标题和上下文。 |
| 文档结构化 | AI 根据会议纪要生成 Markdown 大纲和表格。 | 人工决定保留哪些重点、删除冗余、调整层级。 |
| 技术参数提取 | AI 从 Monad 官方文档提取 RPC、Chain ID、Faucet、Explorer。 | 人工用 JSON-RPC 实测 `eth_chainId`，确认 `0x279f` 与官方文档一致。 |
| 高频场景研究 | AI 协助把“Onchain Quest Arena”拆成 Research / Tech / Ops 三维度。 | 人工选择场景、判断哪些数据上链/不上链、决定 Demo 功能优先级。 |
| x402 / ERC-8004 学习 | AI 协助阅读官方指南、提取参数和合约地址。 | 人工验证 Facilitator `/supported` 接口和 `eth_getCode`，确认地址有 code。 |
| 代码/合约模板 | AI 提供 `Gmonad.sol` 模板和部署步骤。 | 人工决定不自动执行部署，等本人在钱包侧完成签名后回填。 |

---

## 四、我做了哪些人工判断和修改

1. **安全边界优先**：坚持“AI 不接触私钥/助记词”，所有钱包创建、助记词备份、签名操作都由本人完成。项目文件只记录公开地址、交易哈希、网络参数。
2. **来源优先官方文档**：网络参数不照抄社群二手信息，必须从 Monad 官方文档提取，并用 RPC 实测交叉验证。
3. **document-first 流程**：先写计划/文档，再执行，最后回填证据。不把未验证的信息写进提交物。
4. **场景选择判断**：在多个可选方向中，选择“Onchain Quest Arena”作为 Monad 高频交互场景，理由是它最能体现 Monad 0.4 秒出块、高吞吐、低成本的消费级链上应用优势，同时避免“所有数据都上链”的过度设计。
5. **Track 倾向判断**：Week 1 先补齐 Tech 基础（钱包、RPC、交易、合约模板），同时保留 Ops/Research 视角，Week 2 再根据产出能力选主线。

---

## 五、Week 2 方向选择

基于 Week 1 的产出和兴趣分布，建议选择：

**Tech（技术与产品实现）**

理由：
- Week 1 已沉淀大量技术学习材料：网络配置、RPC 实测、合约模板、x402、ERC-8004。
- 已有明确的 Demo 方向：Monad Quest Arena 的链上任务/积分/徽章合约。
- 继续推进可以形成可验证作品：合约地址、交易哈希、GitHub Repo、部署 Demo。

但保留 Ops 和 Research 作为辅助视角：
- Ops：Quest Arena 本身包含社区传播和增长设计。
- Research：x402、ERC-8004、高吞吐链应用场景可继续深挖。

---

## 六、一句话作品集 / 简历说明

> 在 Monad Testnet 上完成钱包配置、RPC 验证与第一笔链上交易，并围绕“高频链上任务与积分系统”输出技术-运营-研究三维度方案，为后续 DApp 开发留下可验证的 Proof of Work。

---

## 七、Week 2 想继续推进的问题

1. 把 `Gmonad.sol` 或 `QuestProof.sol` 真正部署到 Monad Testnet，获得合约地址和交易哈希。
2. 用 Vite + React + wagmi/viem 做一个最小前端，实现：连接钱包、显示余额、调用合约。
3. 验证 x402 在 Monad Testnet 上的支付流程，判断是否适合作为 Quest Arena 的奖励结算层。
4. 找 1-2 位同学试用最小 Demo，收集“哪里不懂、哪里卡住”的反馈。
5. 持续记录 AI 协作边界：AI 生成代码，人工审查、测试、部署和解释。

---

## 八、提交清单

- [ ] 作品链接：`https://github.com/<你的用户名>/Web3SummerInternshipProgram-MonadBuilderCamp/tree/master/submissions/week-01/mini-demo-0.md`
- [ ] Demo 截图 / 录屏 / README：本文件 + 链上交易 Explorer 链接
- [ ] 方向选择：**Tech**
- [ ] 一句话作品集说明：已写
- [ ] Week 2 继续推进的问题：已写

---

## 九、需要你回填的公开信息

请把以下内容直接发给我，我会更新到本文件：

1. 你的 Monad Testnet 钱包地址（公开地址）
2. 你完成的交易类型（转账 / 合约部署 / 合约交互）
3. 交易哈希
4. Explorer 链接
5. 是否确认方向为 Tech，或想改成 Ops / Research？

> 再次提醒：不要发私钥、助记词、API Key、.env 内容或任何未公开会议链接。
