# 项目创意卡片｜Neo（Tech）

> 周次：Week 3｜Day 16 创意收集  
> 角色：Tech / Dev Builder  
> 日期：2026-07-22

---

## 说明

本文件为 Neo 以 Tech 身份提交的项目创意卡片，聚焦 **Monad-native**、**Moss 原生能力**、以及 **较少见的 Agent × 链上方向**。每张卡片均按要求包含：目标用户、痛点、核心功能、Monad 必要性、是否使用 Moss。

团队当前 Mini Demo 锁定方向为「自然语言 swap + Moss Capability simulate + 确认页」，因此创意卡片既作为个人交付物，也为团队后续迭代储备备选方向。

---

## 创意 1：Receipt Chat——把链上交易效果讲成人话

### 目标用户
链上新手、Web2 产品经理、投资者、合规审计员——任何需要**看懂一笔交易实际做了什么**但不想逐行读 ABI 的人。

### 痛点
- 交易签名前，用户看到的是十六进制 calldata 和授权弹窗，无法快速理解「我的钱会怎么动」。
- 交易完成后，Explorer 只列事件日志，普通人无法把日志翻译成「付出了多少、收到了多少、有没有被 MEV」。
- 现有「交易解释」工具多为通用 heuristics，对 DeFi 协议语义（supply/borrow/swap/unwrap）的翻译不准确。

### 核心功能
一个只读 / 插件式解释层：
1. 用户粘贴交易哈希或连接钱包查看待签名交易。
2. 系统通过 Moss `simulate` 跑一遍该交易，拿到 Receipts / Changes。
3. 用 Receipt parser 的结构化 Outcome 生成一段自然语言摘要：
   - "你将用 100 USDC 兑换约 87.3 MON（最小收到 86.1 MON，滑点 0.5%）"
   - "你需要先授权 Kuru Router 使用 100 USDC"
   - "这笔交易会把 0.5 MON 付给验证者作为 gas"
4. 对历史交易，输入 tx hash 即可反查；对待签名交易，直接嵌入钱包弹窗或 DApp 确认页。

### 为什么需要 Monad
- Monad 的低延迟让「粘贴 tx hash → 调用 debug_traceCall → 返回人话摘要」可在 1–2 秒内完成，体验接近 Web2。
- EVM 兼容意味着可以直接复用现有钱包、Explorer、ABI 工具，无需重建生态。
- 链上模拟 + Receipt 解析是 Monad 上才有的原生能力组合（通过 Moss），不是简单爬取 Explorer 文本。

### 是否使用 Moss
**是，且是核心依赖。**
- 用 Moss `action` 重构任意未签名交易对应的 Capability 树。
- 用 Moss `simulate` 拿到按执行顺序排列的 Changes。
- 用 Moss Receipt parser 的 Outcome 作为唯一事实源，避免自己写脆弱的 ABI heuristics。

### 团队可行性（Tech 视角）
- 可复用当前 Mini Demo 的 Kuru swap Capability 和 simulate 链路。
- 前端比 Mini Demo 更简单：一个输入框 + 结果展示页。
- 不需要钱包签名，Demo 风险低。

---

## 创意 2：Moss Capability 沙盒——让协议作者 5 分钟验证一个 Capability

### 目标用户
Monad 生态里的协议开发者、Moss 适配器作者、智能合约审计员、黑客松参赛者。

### 痛点
- 写一个 Moss Protocol adapter 时，开发者需要反复运行 `action → simulate → 检查 Receipt`，但每次都要搭建完整 Registry、Runtime、RPC。
- 没有轻量工具能快速验证「我的 Capability 树结构是否正确、Receipt parser 是否漏了解析事件」。
- 现有测试在 `packages/protocols/*/test/` 里，对新人门槛高，且无法可视化 Capability 树。

### 核心功能
一个面向开发者的沙盒 CLI / Web UI：
1. 用户输入协议名、方法名、参数（JSON 或表单）。
2. 系统调用 Moss `registry.action()` 生成 Capability 树，并以可视化树形展示每个 CapabilityNode 和 TransactionNode。
3. 点击 simulate，系统用 `createTraceSimulator` 执行并展示：
   - 每笔交易的 Changes（Event / nativeTransfer）
   - Receipt 解析结果
   - 任何 Warning（revert、Change 顺序异常、Receipt 解析失败）
4. 支持保存/分享沙盒配置，方便在 GitHub Issue 或 PR 描述中复现问题。

### 为什么需要 Monad
- Moss 是 Monad 原生协议层，沙盒直接服务于 Monad 生态开发者。
- Monad 的低 gas 和低延迟让 simulate 可以实时运行，开发者无需担心 RPC 成本或等待时间。
- 只有 Monad 主网（chainId 143）是 Moss v1 的目标链，沙盒天然聚焦 Monad。

### 是否使用 Moss
**是，100% 基于 Moss 内部 API。**
- Registry 注册 Protocol、注入依赖。
- `action` 生成 Capability 树。
- `simulate` 调用 traceCall 并验证 Receipt。
- 解析结果来自 Receipt parser 的 Outcome 和 ReceiptChange。

### 团队可行性（Tech 视角）
- 可直接基于 `experiments/moss/packages/mcp-server/src/cli.ts` 和 simulator 包改造。
- 前端用树形组件展示 Capability 树即可，技术难度适中。
- 对团队自身价值：我们写 Mini Demo 时已经在 debug Capability 树，这个工具能解决我们自己的痛点。

---

## 创意 3：On-chain 白名单意图信箱——DAO / 社区用自然语言分发可执行的链上操作

### 目标用户
DAO 运营者、社区管理员、空投/激励活动组织者、协议治理参与者。

### 痛点
- DAO 想给成员分发一个「可执行的链上操作」（例如 claim 空投、投票、领取奖励），但成员看不懂合约交互步骤。
- 现有方案要么让成员自己操作（流失率高），要么由多签钱包批量执行（失去个人所有权）。
- 缺少一种「运营者发布意图，成员一键确认并签名」的轻量机制。

### 核心功能
一个意图发布与执行平台：
1. 运营者在后台用自然语言或结构化表单发布一个「意图卡片」：
   - "领取本周社区贡献奖励 50 USDC"
   - "对提案 #12 投赞成票"
2. 平台将意图转换为 Moss Capability 树，并用某白名单地址（如 DAO 多签或 merkle 证明）限制可执行者。
3. 普通用户打开卡片，看到人话解释和simulate 结果，点击确认后用自己的钱包签名广播。
4. 运营者可追踪哪些成员已完成，哪些已读未签。

### 为什么需要 Monad
- DAO 工具在 Monad 上几乎空白，存在生态空白。
- 低 gas 让「发布大量小额意图卡片」经济可行。
- 高吞吐让成员集中执行时不会出现网络拥堵。

### 是否使用 Moss
**是。**
- 用 Moss 把运营意图转成可验证 Capability 树。
- 用 simulate 在用户端展示真实效果，降低「这个 claim 会不会盗我资产」的恐惧。
- 白名单/merkle 验证是额外的合约层，Moss 负责可执行交易的安全展示。

### 团队可行性（Tech 视角）
- 比 Mini Demo 多一个后台发布页和一个白名单合约，复杂度中等。
- 若时间有限，可把「白名单」改为硬编码地址列表或签名者列表。
- 演示冲击力强：3 分钟展示「运营者发意图 → 用户看懂 → 一键签名」。

---

## 创意 4：链上 Receipt 保险柜——自动保存并结构化你的每一笔 DeFi 交互记录

### 目标用户
活跃 DeFi 用户、税务申报者、投资组合追踪者、审计员。

### 痛点
- 用户在多个 DApp 操作后，没有统一、结构化、可验证的历史记录。
- 现有 portfolio tracker 大多读取 Transfer 事件，无法理解 supply/borrow/repay/swap 等业务语义。
- 税务/审计时需要手动整理每笔交易的实际经济效果。

### 核心功能
一个用户个人的链上 Receipt 保险柜：
1. 用户连接钱包，系统自动扫描其地址在 Monad 上的历史交易。
2. 对每笔涉及已知协议（Kuru、Neverland 等）的交易，调用 Moss Receipt parser 解析业务语义。
3. 生成结构化记录：时间、协议、动作、资产流入流出、gas 成本、滑点/价格影响。
4. 支持导出 CSV / JSON，用于税务或分析。
5. （可选）对未签名交易提供「模拟后再执行」模式，帮助用户在执行前理解效果。

### 为什么需要 Monad
- Monad 交易历史可完整追溯，低 gas 鼓励高频交互，用户更需要自动化记录工具。
- EVM 兼容让现有地址、交易格式、Explorer 数据可直接复用。
- 在 Monad 上这类工具几乎空白，率先占位有生态卡位价值。

### 是否使用 Moss
**是。**
- 用 Moss Protocol 的 Receipt parser 解析历史交易 Changes。
- 用 Query 读取用户当前余额/仓位作为补充。
- 用 simulate 验证待执行交易的效果（若实现模拟模式）。

### 团队可行性（Tech 视角）
- 解析历史交易需要 indexer 或遍历区块，复杂度高于 Mini Demo。
- 可简化：只支持用户手动输入 tx hash 或只展示最近 N 笔交易。
- 长期价值高，但不太适合本周 Mini Demo。

---

## 创意优先级（供团队讨论）

| 优先级 | 创意 | 与当前 Mini Demo 的关系 | 本周可行性 |
|--------|------|------------------------|------------|
| P0 | 创意 1：Receipt Chat | 直接延伸当前 Demo 的确认页解释能力 | 高 |
| P1 | 创意 2：Moss Capability 沙盒 | 解决我们自己开发调试的痛点 | 中高 |
| P2 | 创意 3：DAO 意图信箱 | 开辟新用户群（DAO 运营者） | 中 |
| P3 | 创意 4：链上 Receipt 保险柜 | 长期工具，需 indexer | 低 |

---

## 关联文档

| 文档 | 路径 |
|------|------|
| 团队 Mini Demo 问题定义 | `submissions/week-03/problem-statement.md` |
| Mini Demo 范围 | `submissions/week-03/mini-demo-scope.md` |
| Dev 角色验证 | `submissions/week-03/dev-role-validation.md` |
| Idea Pitch | `submissions/week-03/idea-pitch.md` |
