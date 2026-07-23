# 团队决定与 AI 使用记录｜Moss Mini Demo Squad

> 任务：Week 3｜记录团队决定与 AI 使用情况  
> 团队：Moss Mini Demo Squad  
> 成员：Neo（Dev / Tech Lead）、Riso（PM / Pitch）、eleven（UI / 视觉）  
> 整理人：Neo  
> 日期：2026-07-23  
> 状态：Day 3 结束时更新，Day 4–Day 5 持续补充

---

## 团队做出的重要决定

### 1. 锁定 Mini Demo 方向：自然语言 swap 确认助手

**内容**：用户输入「swap 100 USDC to MON on Monad」→ Agent 解析意图 → Moss Kuru Capability 树 + simulate → 可理解确认页 → 用户签名。

**团队成员**：全体（Neo 提出技术可行性，Riso 控制范围，eleven 确认界面可讲懂）。

**为什么这样决定**：
- 问题真实：链上新手面对 Agent 返回的 Capability 和授权弹窗存在明确恐惧。
- 团队能力匹配：Neo 已本地跑通 Moss Kuru swap + simulate，三人分工刚好覆盖最小交付。
- 本周可展示：只验证一条 swap 链路，3 分钟 Demo 即可讲完。
- Monad 原生：低延迟让「说完意图 → 秒级 simulate → 展示结果」的体验成立；Moss 是 Monad 生态原生协议层。

---

### 2. 明确安全边界：Moss 只做规划与模拟，不自动签名/广播

**内容**：任何资产操作必须有用户明确确认步；项目不托管私钥、助记词；Demo 中签名由用户的钱包完成。

**团队成员**：全体（Riso 提出，Neo 确认技术可实现，eleven 在确认页中体现）。

**为什么这样决定**：
- 这直接回应了「AI Agent 会不会自动转走资产」的用户疑虑。
- 在本周时间有限的情况下，这种设计避免了私钥管理和后端托管带来的安全与合规复杂度。
- 符合 Moss 新架构的本意：Capability 和 TransactionNode 是未签名的，需要用户最终授权。

---

### 3. 自然语言解析使用预置模板，不接 LLM

**内容**：用户输入「swap 100 USDC to MON」被映射为结构化参数，而不是调用 LLM 解析。

**团队成员**：Neo（Dev）提出，Riso（PM）同意，因为不影响核心假设验证。

**为什么这样决定**：
- 本周核心假设是「用户看懂 Capability Receipt 后更愿意签名」，而不是「LLM 意图理解是否准确」。
- 预置模板可以在几分钟内稳定演示，避免 LLM 幻觉和网络不稳定。
- 若有余力，可在 Week 4 替换为 LLM，但不影响本周 Demo。

---

### 4. 确认页信息层级以「付出 / 收到 / 风险」三块为核心

**内容**：不展示原始 ABI 或 calldata，而是用三个可视化区块呈现最关键信息。

**团队成员**：eleven（UI）提出，Riso（PM）与 Neo（Dev）确认技术字段可提供。

**为什么这样决定**：
- 用户测试的核心问题是「看不懂该看什么」，而不是「信息不够」。
- 三块结构直接对应用户的经济心理模型：我给了什么、我能得到什么、有什么潜在损失。

---

## 删除或暂时不做的功能

| 功能 | 删除/暂时不做的原因 | 是否会在未来重新讨论 |
|---|---|---|
| 多个 DEX / 多协议对比 | 本周只验证一条 swap 链路 | 是，Week 4 可拓展 |
| 自动签名/自动执行 | 安全边界：必须保留用户确认 | 否，资产操作必须用户授权 |
| 多链支持 | 只关注 Monad，本质上是 Moss v1 的目标链 | 否，Moss v1 是 Monad-mainnet only |
| 借贷/质押/多步交互 | 超出本周范围 | 是，Week 4 可考虑 |
| 链上 Receipt 事后对账 | 需要 indexer，本周无法出 Demo Evidence | 是，长期方向 |
| DAO / 白名单意图信箱 | 需要额外合约和后台，超出本周范围 | 是，Week 4 Hackathon 备选 |
| Moss Capability 沙盒（开发者工具） | 本周优先用户故事，开发者工具优先级次之 | 是，Week 4 备选 |
| LLM 自然语言理解 | 预置模板足以验证核心假设 | 是，有余力时替换 |

---

## AI 帮助完成了什么

### Neo（Dev / Tech Lead）：
- 使用 Cursor / Claude Code 初始化 Vite + React + wagmi 项目骨架，并生成 Moss 调用的基础模板。
- 让 AI 帮忙解读 Moss `packages/protocols/kuru/src/kuru.ts`、`packages/simulator/src/simulator.ts` 的接口，提取出 `action` 与 `simulate` 的使用范例。
- 让 AI 生成确认页的 CSS 布局草稿，再由 eleven 调整信息层级和视觉风格。
- 未让 AI 生成任何需要接入私钥、签名逻辑的代码；钱包操作由自己写完并审查。

### Riso（PM / Pitch）：
- 使用 AI 快速梳理 Biconomy、DeFiSaver、Zapper 等竞品的公开信息，初步形成竞品模板。
- 使用 AI 起草项目一句话介绍和测试邀请文案，再由全队一起修改定稿。
- 没有让 AI 代替决策；范围、优先级、安全边界由团队讨论后确定。

### eleven（UI / 视觉）：
- 使用 AI 生成 3 屏主路径的线框草稿，作为讨论起点。
- 使用 AI 梳理 DeFi 确认页设计模式（如 Uniswap 等），帮助确定信息层级。
- 最终设计稿由 eleven 自己完成，确保与团队品牌和 Demo 效果一致。

### 全队共同：
- 用 AI 辅助生成会议纪要、竞品分析模板、用户测试问题草稿，但所有最终文档由团队成员审查后发布。

---

## 团队进行了哪些检查或修改

- **技术可行性检查**：Neo 验证了 Moss Kuru swap Capability 本地可以生成未签名 TransactionNode，并且 simulate 能返回包含 Changes 的 Receipt，确认方向可行。
- **安全边界审查**：全队确认 Demo 中不会保留私钥、助记词，不自动广播；钱包签名由 wagmi/rainbowkit 标准流程完成。
- **范围审查**：Riso 在每日 stand-up 中将新需求（如是否加上 price impact、是否做多个 swap 模板）与 Must Have 清单对照，超出范围的列入 Nice to Have。
- **文档一致性检查**：确保 `team.md`、`team-submission.md`、`problem-statement.md`、`mini-demo-scope.md`、`brainstorm-meeting.md`、`team-plan.md` 中的团队成员、方向、范围描述一致。
- **视觉检查**：eleven 确认确认页不展示原始 ABI，只展示「付出 / 收到 / 风险」，并在线框阶段反馈给 Neo。
- **AI 输出审查**：任何 AI 生成的代码、文案、设计草稿都经过相应负责人审阅，不会直接使用未审查的 AI 产出。

---

## 当前遇到的问题

### 1. 随队友 Riso、eleven 的进度尚不清晰
- **说明**：由于微信群异步沟通，尚未收到 Riso 的竞品分析和 eleven 的线框稿定稿。
- **影响**：可能导致 Day 4 集成时视觉对不齐，或用户测试洼招募延迟。
- **应对**：在今晚 stand-up 中确认各自交付物状态，若缺席则发异步三句。

### 2. Kuru mainnet simulate 稳定性未完全验证
- **说明**：本地可以跑通，但未在多个 RPC 或网络环境下测试。
- **影响**：Demo 时可能出现 simulate 超时或返回空 Receipt。
- **应对**：准备离线 mock 数据作为 fallback，确保 UI 和 Demo 路径可以离线演示。

### 3. 钱包签名广播的调试时间不确定
- **说明**：如果 mainnet 签名广播出现问题，需要足够时间切换到「展示待签名交易」的降级方案。
- **影响**：可能影响 Demo Evidence 的质量（无法留下真实交易哈希）。
- **应对**：先实现待签名展示，广播作为 Nice to Have，并预留 2 小时调试缓冲。

---

## 下一步准备做什么

| 下一步 | 负责人 | 截止 |
|---|---|---|
| 在 stand-up 中确认 Riso、eleven 的交付物状态 | Riso / eleven / Neo | 7/23 21:15 |
| 完成竞品分析 | Riso | 7/23 21:00 |
| 落实测试用户名单 | Riso | 7/23 21:00 |
| 完成 3 屏线框定稿 | eleven | 7/23 21:00 |
| 搭建好前端骨架 | Neo | 7/23 12:00 |
| 实现意图解析模板 | Neo | 7/23 18:00 |
| 接入 Moss simulate 并与 UI 对齐 | Neo + eleven | 7/24 12:00 |
| 完成用户测试并形成反馈记录 | 全队 | 7/24 21:00 |
| 录制 Demo 并准备 Pitch 素材 | 全队 | 7/25 12:00 |
| 根据本文档持续更新决定与 AI 使用记录 | Neo | 7/25 复盘后 |

---

## 关联文档

| 文档 | 路径 |
|------|------|
| 脑暴会议记录 | `submissions/week-03/brainstorm-meeting.md` |
| 团队计划 | `submissions/week-03/team-plan.md` |
| 问题定义 | `submissions/week-03/problem-statement.md` |
| Mini Demo 范围 | `submissions/week-03/mini-demo-scope.md` |
| 团队构建计划 | `submissions/week-03/build-plan.md` |
