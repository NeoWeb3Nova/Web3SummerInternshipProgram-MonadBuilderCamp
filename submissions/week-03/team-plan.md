# 团队计划｜Moss Mini Demo Squad

> 任务：Week 3｜制定团队计划  
> 日期：2026-07-23  
> 团队：Moss Mini Demo Squad  
> 成员：Neo（Dev / Tech Lead）、Riso（PM / Pitch）、eleven（UI / 视觉）  
> 基于：`submissions/week-03/brainstorm-meeting.md` 会议结论

---

## 团队本周目标

Friday（7/24）之前做出一条可演示的 swap 链路，并留下 Demo Evidence：

> 用户输入「swap 100 USDC to MON on Monad」→ Agent 解析意图 → Moss Kuru Capability 树 + simulate → 可理解的确认页 → 用户确认后触发钱包签名（至少展示待签名交易，尽量广播）。

---

## 工作分配与具体成果

| 要完成的事情 | 负责人 | 具体成果 | 截止时间 | 协作对象 |
|---|---|---|---|---|
| 了解用户与类似产品 | Riso | 完成 2 款竞品分析：1）通用 AI Agent 钱包签名解释（如 Biconomy / Privy、Grok / ChatGPT 钱包助手）；2）DeFi 确认页解释层（如 DeFiSaver、Zapper、Fire），形成 `submissions/week-03/competitor-analysis.md` | 7/23 21:00 | Neo（确认 Moss 能力边界） |
| 准备项目介绍和测试邀请 | Riso | 输出 50 字以内项目一句话介绍，以及用于社群招募的测试邀请文案，同时落实 3–5 位测试用户联系方式 | 7/23 21:00 | 全队（审阅文案） |
| 制作核心功能（前端与 Moss 链路） | Neo | 输出可运行的 Vite + React + wagmi 项目，实现：自然语言意图解析 → Kuru Capability 生成 → simulate 返回 Receipt → 确认页 → 钱包签名（代码仓位于 `experiments/week-03-prototype/`） | 7/24 18:00 | eleven（UI 交互对齐） |
| 设计确认页与 Demo 演示视觉 | eleven | 输出 3 屏主路径线框或高保真：输入屏 → Receipt/simulate 结果屏 → 确认屏；并在 Day 4 与 Neo 对接落地到代码 | 7/23 21:00（线框）<br>7/24 12:00（对齐完成） | Neo（技术可行性） |
| 邀请用户测试 | 全队 | 形成 `submissions/week-03/user-feedback.md`，记录 3 位以上用户的：1）是否看懂 Capability Receipt；2）是否敢点确认；3）是否理解风险 | 7/24 21:00 | Riso（策划测试问题） |
| 准备 Demo 展示 | 全队 | 输出 60–90 秒 Demo 录屏、3 分钟 Pitch 提纲和 Demo 剧本，形成 `submissions/week-03/demo.md` 与 `submissions/week-03/pitch-outline.md` | 7/25 12:00 | Riso（Pitch） + eleven（视觉） + Neo（技术证据） |
| 生成 Demo Evidence | Neo | 至少一项可验证产出：测试网交易哈希 / 合约地址 / 可运行网页 / 60–90 秒录屏 | 7/25 12:00 | 全队（审阅证据） |

---

## 成员具体责任

### Neo（Dev / Tech Lead）

- 搭建前端项目骨架：Vite + React + wagmi，位于 `experiments/week-03-prototype/` 。
- 实现自然语言意图解析（预置模板，不用 LLM）。
- 接入 Moss Kuru `swap` Capability 生成与 `simulate` 调用。
- 实现确认页，展示：token in / token out / estimated out / minimum out / 滑点 / 授权 / 风险提示。
- 实现钱包签名触发（至少展示待签名交易，尽量完成广播）。
- 生成 Demo Evidence（交易哈希 / 合约地址 / 录屏）。

### Riso（PM / Pitch）

- 完成 2 款竞品分析，落地为 `submissions/week-03/competitor-analysis.md`。
- 制定 50 字以内项目一句话介绍与测试邀请文案。
- 招募并落实 3–5 位测试用户，准备 5 个用户测试问题。
- 在 Day 4 组织用户测试，形成 `submissions/week-03/user-feedback.md`。
- 起草 3 分钟 Pitch 提纲和 Demo 剧本，落地为 `submissions/week-03/pitch-outline.md`。
- 控制范围：本周不做多协议、多链、借贷、DAO 、自动执行。

### eleven（UI / 视觉）

- 设计 3 屏主路径线框 / 高保真：输入屏 → Receipt/simulate 结果屏 → 确认屏。
- 确认页信息层级以「付出 / 收到 / 风险」三块为核心，确保非技术用户能看懂。
- 与 Neo 对接设计稿落地到代码。
- 准备 Demo 录屏素材（动画过渡、问题/方案/演示/为什么 Monad 四段）。
- 在 Day 5 前输出 60–90 秒 Demo 录屏。

---

## 时间节点

| 日期 | 里程碑 | 负责人 |
|---|---|---|
| 7/23 12:00 | 前端项目骨架搭建完成 | Neo |
| 7/23 18:00 | 意图解析预置模板实现 | Neo |
| 7/23 21:00 | 竞品分析完成 + 3 屏线框定稿 + 测试者落实 | Riso + eleven |
| 7/24 12:00 | 接入 Moss simulate 并完成确认页 UI 对齐 | Neo + eleven |
| 7/24 18:00 | 核心链路可跑通（意图 → Capability → simulate → 确认 → 签名） | Neo |
| 7/24 21:00 | 完成用户测试并形成反馈记录 | 全队 |
| 7/25 12:00 | Demo 录屏 + Pitch 提纲 + Demo Evidence 齐 | 全队 |
| 7/25 18:00 | 团队复盘 `submissions/week-03/retro.md` 完成 | Riso |

---

## 沟通与协作

- 每日 stand-up：21:00–21:15 UTC+8，微信群。
- 缺席 stand-up 时需在群里发异步三句：昨日完成 / 今日计划 / 当前卡点。
- 技术问题找 Neo；范围、进度、用户测试找 Riso；界面与 Demo 观感找 eleven。
- 所有交付物在 `submissions/week-03/` 和 `experiments/week-03-prototype/` 中维护，推送前在群里 @ 对应负责人 review。

---

## 本周不做

- 不接多个 DEX 或多个协议（只用 Kuru）。
- 不实现自动执行、自动签名、自动策略。
- 不托管用户私钥或助记词。
- 不做多链、不做借贷/质押/多次交互。
- 不用真实 LLM 做自然语言解析（用预置模板降级）。
- 不做链上 Receipt 事后对账（Demo 做到广播/待签名为止）。

---

## 风险与应对

| 风险 | 应对 | 负责人 |
|---|---|---|
| Kuru mainnet simulate 不稳定 | 先用离线 mock 验证 UI 与逻辑，再切 mainnet | Neo |
| 钱包签名调试耗时 | 先做到展示待签名交易，再补广播 | Neo |
| UI 进度滞后 | eleven 先出线框，Neo 用简单表单先跑通功能 | eleven + Neo |
| 测试用户找不到 | Riso 提前在 Builder 群和社区发招募消息 | Riso |
| 范围膨胀 | Riso 每日 stand-up 检查 Must Have 完成度，新需求需经全体同意 | Riso |

---

## 关联文档

| 文档 | 路径 |
|------|------|
| 脑暴会议记录 | `submissions/week-03/brainstorm-meeting.md` |
| 问题定义 | `submissions/week-03/problem-statement.md` |
| Mini Demo 范围 | `submissions/week-03/mini-demo-scope.md` |
| 团队构建计划 | `submissions/week-03/build-plan.md` |
| Tech 创意卡片 | `submissions/week-03/idea-cards-neo.md` |
