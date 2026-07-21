# Team Formation Card

> 周次：Week 3｜Builder Collaboration  
> 日期：2026-07-20  
> 状态：已组队（3 人）  
> 关联：`team.md` · `team-working-agreement.md` · `idea-pitch.md`

---

## 1. 小队一览

| 项 | 内容 |
|----|------|
| **队名（暂定）** | Moss Mini Demo Squad（可改） |
| **人数** | 3 |
| **主方向** | Moss-powered DeFi Agent Mini Demo |
| **一句话目标** | 本周做出「自然语言意图 → Moss Capability 树 + simulate → 用户可理解的确认界面」的可演示最小链路，并留下可检查 Demo Evidence |

### 术语对照

- **Capability 树**：Moss 新架构中代替旧 `Plan` 的未签名交易组织形式；每个 Capability 拥有一个直接 TransactionNode 和一个 Receipt 解析器，嵌套的 Capability 由 core 深度优先展平。
- **Receipt / Changes**：simulate 后产生的有序原始事件与资产变化，Receipt 解析器将其翻译成可读文本。
| **后续意向** | 若 Mini Demo 反馈 OK，共同评估进入 Week 4 Hackathon |

---

## 2. 成员 · 角色 · 联系方式

> 请把 `待填` 换成真实昵称 / 微信 / GitHub，提交学习平台前务必补齐。

| 角色 | 姓名 / 代号 | Track 对应 | 本周投入（估） | 联系方式 | 主责 |
|------|-------------|------------|----------------|----------|------|
| **Dev / Core** | Neo | Tech | 25–30h | 微信：`Web3-Nova-Neo` · GitHub：[NeoWeb3Nova](https://github.com/NeoWeb3Nova) | 合约 / 前端 / Moss、测试部署、链上证据 |
| **项目经理 PM** | Riso | Ops / Pitch（推进） | 待确认 h | 微信：待确认 · 其他：待确认 | 范围、节奏、看板、决策记录、Pitch 结构 |
| **UI** | eleven | Ops / 设计 | 待确认 h | 微信：待确认 · 作品集：待确认 | 信息架构、界面、演示视觉、确认页可读性 |

### 角色与任务手册的映射

| 手册角色 | 本队谁扛 |
|----------|----------|
| Tech Lead | Neo |
| PM / Pitch 推进 | PM |
| Ops（用户测试、内容、Demo 执行） | PM 主导 + UI 协助 |
| Research（问题论证、竞品、叙事论据） | PM 主导 + Neo 技术论据 |
| 视觉 / 界面 | UI |

---

## 3. 共同目标（本周）

### 必须做到（Definition of Done · Mini Demo）

- [ ] 有清晰用户与痛点（Problem & User Card）  
- [ ] 只保留 **一条** 端到端链路，砍掉其余  
- [ ] 链路可演示：意图输入 → Capability / simulate 结果 → 确认态  
- [ ] 至少一类 **Demo Evidence**：合约地址 / 交易哈希 / 可运行 Repo / 录屏 之一（优先多类）  
- [ ] 3 分钟 Pitch 能讲完：问题 → 方案 → 演示 → 为什么 Monad → 下一步  
- [ ] 至少 1–3 人试用或看过 Demo 并留下反馈  

### 明确不做什么（本周）

- 不做通用多协议 Agent  
- 不做自动执行 / 托管私钥 / 无人值守策略  
- 不做多链  
- 不追求完整产品与增长漏斗  

---

## 4. 组队对齐检查（Day 1 已确认项）

| 检查项 | 结论 |
|--------|------|
| 是否对同一用户问题感兴趣 | ✅ 默认对齐 Idea Pitch（DeFi 新手 × Moss 安全确认）；Day 2 可微调措辞 |
| 时间投入与沟通节奏是否匹配 | ⏳ 三人需填入投入小时；默认晚间 15 分钟同步 |
| 是否有人负责推进和记录 | ✅ **PM** 主责看板与纪要；Neo 补技术证据 |
| 是否至少有人能完成可检查 Demo Evidence | ✅ **Dev（Neo）** 主责；UI 负责可展示界面证据 |
| 对「本周做到什么程度」是否有共同预期 | ⏳ 写入本文 DoD；Day 2 在 Solution Design / Build Plan 再收紧一次 |

---

## 5. 协作工具

| 用途 | 工具 | 负责人 |
|------|------|--------|
| 代码与 PR | GitHub（本仓库 + Demo 子目录 / 独立 Repo） | Dev |
| 任务看板 | GitHub Projects 或 Notion（二选一，PM 定） | PM |
| 即时沟通 | 微信群（队内专用） | 全员 |
| 设计稿 | Figma / 本地线框 / 截图（UI 选） | UI |
| 文档沉淀 | 本仓库 `submissions/week-03/` | 全员 |

---

## 6. 本周节奏（摘要，细则见 Working Agreement）

| 日 | 焦点 | 主要产出 |
|----|------|----------|
| Day 1（今） | 认识彼此、组队 | Profile · Pitch · Formation · Agreement |
| Day 2 | 问题与范围 | Problem Card · Scope · Monad Fit · Solution Design / Build Plan |
| Day 3 | 实现与交接 | 一条链路跑通或可模拟 + UI 主路径 |
| Day 4 | 反馈与迭代 | Feedback Log · 修最伤展示的问题 |
| Day 5 | Demo 与复盘 | Demo 脚本 · Pitch · Retro · Hackathon 意向 |

---

## 7. 风险与依赖

| 风险 | 缓解 |
|------|------|
| 核心动作选太久 | Day 2 晚间必须锁定一个动作 |
| Moss / 主网 e2e 环境不稳 | Dev 先 CLI 打通，UI 可对 Mock 数据排版 |
| 三人投入落差 | PM 按「最小可演示」排优先级，不强求完美 UI |
| 成员名未写入文档 | 今日内补齐本卡「待填」字段再交平台 |

---

## 8. 签名确认（组队成立）

| 成员 | 同意共同目标与安全边界 | 日期 |
|------|------------------------|------|
| Neo（Dev） | ✅ | 2026-07-20 |
| Riso（PM） | ⏳ 确认后勾选 | |
| eleven（UI） | ⏳ 确认后勾选 | |
