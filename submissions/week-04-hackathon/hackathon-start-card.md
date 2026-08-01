# Hackathon Start Card｜Week 4 Day 5

> 学分：+30  
> 用途：把 Idea 收敛为「下一周第一个可演示的核心动作」  
> 原则：不排满功能清单；只承诺一个可被体验、解释、检查的版本  
> 日期：2026-08-01  
> 提交人：Neo（代表团队 Riso / Neo / Eleven）

---

## 项目快照

| 字段 | 内容 |
|------|------|
| **项目名（可暂定）** | **硅基劳动仲裁院 Silicon Labor Arbitration**（SLA · The Unfinished Verdict｜未完成的判决） |
| **日期** | 2026-08-01 |
| **用户是谁** | 委托 AI Agent 完成任务（链上或链下）的个人用户，以及交付出问题时需要查明责任的 Agent 开发者 / 委托方。 |
| **用户问题（一句话）** | 当人类把行动委托给 AI Agent 链时，出事后每一环都有免责理由，责任在委托链中消失；委托人需要一条可核验的责任时间线，而不是一份 AI 单方给出的判决书。 |
| **Demo 核心动作** | 用户只完成这一件事：**作为委托人，发起一次「土豆案」仲裁**——支付 0.2 MON 创建带验收条件（C1–C4）的任务 → Agent 交付「土豆」→ 用户点击「发起争议」→ 看到规则层自动结算客观条款（C1–C3）、主观条款（C4「是一只猫」）冻结转人工终审。 |
| **完成后的价值** | 用户得到一条可核验的链上责任时间线（任务 → 交付 → 争议 → 规则判定 → 结算/冻结 → 人工终审），清楚看到哪些由系统自动判定、哪些诚实移交人类终审——而不是一份不可上诉的 AI 终审判决。 |

---

## 真实运行 vs Mock

| 必须真实运行 | 可先 Mock / Figma / 现成组件 / 人工流程 |
|--------------|----------------------------------------|
| `TaskEscrow` 合约（Monad Testnet 已部署 `0x67040374b8A9756586De0885f01d1291cE8FFCcF`）全生命周期：`createTask → assignAgent → submitDelivery → acceptDelivery / openDispute → settle → releaseFrozen` | 前端 UI（Next.js + typed mock adapter）：先用 mock 数据驱动页面，再接 live 合约 |
| Moss `createTask`（vendor/moss `silicon-arbitration` Protocol + MossBridge）：构造未签交易 → Testnet 模拟（无 Warning）→ 生成 E3 签前证据 | `EvidenceRegistry` 合约（未实现，决策 pending）：本轮用 E3 链下证据 + 链上事件替代，不新部署 |
| 确定性规则引擎（`packages/rules`）：C1–C4 判定 + `weightBps` 分账推导 | 钱包签名：现成测试网钱包（MetaMask / wagmi hooks） |
| AI 三路意见（`packages/ai`）：检方 / 辩方 / 审计，必须引用证据编号，结构上不能决定金额（Gonka 已跑通并固化 fixture） | 人工终审页面：先以脚本 / 管理端动作模拟 human review，再接入界面 |
| 真实交易哈希 + 部署证据（`deployments/monad-testnet.json`，bytecode/ABI hash 已核验） | 20–50 并发案件统计：仅展示真实 tx hash 与 gas，不做推断性性能声明 |

---

## Monad / Moss

| 字段 | 内容 |
|------|------|
| **为什么适合 Monad** | 每个 `caseId` / `taskId` 都是**独立状态**、案件之间不争用全局变量；Monad 的低延迟高并行让未来数千个 Agent 微任务的争议可以低成本、并行进入证据提交、审查与结算——**Monad 的意义不是让单个案件更复杂，而是让争议规模化处理成为可能**。 |
| **是否使用 Moss** | **是** |
| **若使用 Moss** | Moss 覆盖 `createTask`：把自然语言任务委托构造成未签名 Capability 交易 → 在 Monad Testnet 模拟（`Reverted: false | Gas: 217,941 | Warnings: 0`）→ 把用户看到的签前解释原文、Capability、模拟 Receipt、Moss/Protocol/ABI 版本与 canonical hash 一起组成案件第一份证据 **E3**。Moss 是事前解释，仲裁院是事后追责——**E3 是连接两者的证据链**。后续 `assignAgent / submitDelivery / openDispute / settle` 走 viem 直接调用，明确不标记为 Moss verified。 |

---

## 下周最先验证的风险

| 字段 | 内容 |
|------|------|
| **头号风险类型** | **技术** |
| **风险描述** | 合约、Moss 模拟、规则引擎、AI 层均已跑通，但**前端 UI 尚未落地**（Next.js + typed mock adapter 仍是规划模块）。两周内最大的不确定：能否把已跑通的后端链路接成真人可点、评委可看的完整 Demo 闭环。 |
| **如何在 1 周内用最小动作验证** | Eleven 出主路径线框（下单 → 交付 → 争议 → 结算/冻结 → 人工终审）；Neo 用 typed mock adapter 先跑通五屏数据流，再接一次**真实 `createTask` + 真实 `settle`**，验证 E3 与链上事件在 UI 上的呈现；Riso 用土豆案话术对 3 位同学做一轮可理解性测试（30 秒能否看懂「自动判定 vs 冻结转人工」）。 |

---

## 团队与帮助

| 字段 | 内容 |
|------|------|
| **成员与角色** | **Riso**：产品 · 规则引擎 · AI 层 · 统筹；**Neo**：合约 · Moss · 链上集成；**Eleven**：UI · 视觉 · 交互 |
| **当前阻塞** | 无硬阻塞。前端 UI 与 `EvidenceRegistry` 决策（本轮明确不做，用 E3 链下证据替代）是剩余缺口。 |
| **需要的帮助** | 有 Next.js / wagmi 经验的同学可加速 UI 落地（加分非阻塞）；若导师有「仲裁 ≠ 法院、人保留终审」叙事的一轮反馈会很有价值。 |
| **是否进入 Build Sprint** | **是**（条件就绪：合约已部署 Testnet、Moss live simulation 已通过、规则引擎与 AI 意见已固化） |

---

## 90 秒 Check-in 脚本（可选草稿）

| 时段 | 内容 |
|------|------|
| 30 秒 · 用户与问题 | 人类委托 Agent 干活，出事后每一环都有理由——「我没让它这样做」「我只是执行参数」——最后责任消失了。我们做硅基劳动仲裁院：**AI 只解释，人保留终审**。 |
| 30 秒 · 核心动作 | Demo 里，用户支付 0.2 MON 委托 Agent「画一只适合儿童产品的橙色猫，PNG、透明背景、中午前交付」。Agent 交付了一颗土豆。用户发起争议，规则层自动结算时间/格式/透明背景三项，但「是不是猫」冻结转人工终审——**系统诚实地说：我判不了 C4，你来判**。 |
| 30 秒 · 团队 / 阻塞 / 需要帮助 | 三人团队：Riso 管规则与 AI 层，Neo 管合约与 Moss，Eleven 管 UI。合约已部署 Monad Testnet、Moss 模拟已跑通；当前阻塞是前端 UI 未落地，欢迎有 Next.js 经验的同学加入或给反馈。 |

听众建议 / 可用资源（记录一条）：

---

## 自检

- [x] 只有一个核心动作（发起一次土豆案仲裁），没有「第二周功能大全」
- [x] 真实 vs Mock 边界写清（合约/Moss/规则引擎真实；UI/EvidenceRegistry Mock）
- [x] 写明头号风险（技术：前端 UI 未落地），而不是乐观假设全成
- [x] 团队知道下周第一步是什么（线框 → typed mock 五屏 → 一次真实 createTask + settle）

---

## 关联文档

| 文档 | 路径 |
|------|------|
| 项目仓库 | `https://github.com/LierMi/Silicon-Labor-Arbitration`（README · docs/01–09） |
| 技术风险与决策清单 | 项目仓库 `docs/06-技术风险与决策清单.md`（Gate 1–10 决策门） |
| 部署证据 | 项目仓库 `deployments/monad-testnet.json`（chain 10143） |
| Week 3 问题与方案 | `../week-03/problem-statement.md` |
| Reality Check（Day 4） | `reality-check.md` |
