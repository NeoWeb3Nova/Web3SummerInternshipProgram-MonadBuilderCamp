# 团队脑暴会议记录｜Moss Mini Demo Squad

> 任务：Week 3｜组织一次团队脑暴会议  
> 会议时间：2026-07-22 21:00–21:40 UTC+8（约 40 分钟）  
> 参与成员：Neo（Dev / Tech Lead）、Riso（PM / Pitch）、eleven（UI / 视觉）  
> 记录人：Neo  
> 状态：已结束，方向已锁定

---

## 一、会议流程

| 阶段 | 时长 | 内容 |
|------|------|------|
| 提出想法 | 10 分钟 | 每位成员轮流提出至少 1 个想法，只记录、不评价 |
| 整理想法 | 10 分钟 | 合并相似想法，补充目标用户、痛点、解决方式 |
| 讨论筛选 | 10 分钟 | 从问题真实性、团队能力、本周可展示性三方面评估 |
| 确定方向 | 10 分钟 | 投票锁定最终方向，记录暂时放弃的想法与下一步行动 |

---

## 二、每位成员提出的想法

### Neo（Dev / Tech Lead）

1. **Receipt Chat——把链上交易效果讲成人话**  
   目标用户：链上新手、Web2 PM、合规审计员。  
   痛点：交易签名前看到的是 calldata 和授权弹窗，看不懂「我的钱会怎么动」；交易完成后 Explorer 只有事件日志。  
   解决方式：用 Moss `simulate` 跑交易，再用 Receipt parser 把 Changes 翻译成自然语言摘要。

2. **Moss Capability 沙盒——让协议作者 5 分钟验证一个 Capability**  
   目标用户：Monad 协议开发者、Moss 适配器作者、黑客松参赛者。  
   痛点：写 Moss adapter 时需要反复跑 `action → simulate → 检查 Receipt`，但每次都需搭 Registry / Runtime / RPC。  
   解决方式：做一个 Web UI / CLI，输入协议方法参数即可生成 Capability 树、运行 simulate、展示 Receipt 与 Warning。

3. **On-chain 白名单意图信箱——DAO / 社区用自然语言分发可执行的链上操作**  
   目标用户：DAO 运营者、社区管理员、空投/激励组织者。  
   痛点：DAO 想给成员分发可执行链上操作（claim 奖励、投票），但成员看不懂步骤；批量执行又失去个人所有权。  
   解决方式：运营者发布意图卡片，平台转成 Moss Capability 树 + 白名单限制，用户看到人话解释和 simulate 结果后一键签名。

4. **链上 Receipt 保险柜——自动保存并结构化用户的每一笔 DeFi 交互记录**  
   目标用户：活跃 DeFi 用户、税务申报者、投资组合追踪者。  
   痛点：portfolio tracker 只读 Transfer 事件，无法理解 supply/borrow/repay/swap 等业务语义。  
   解决方式：用 Moss Receipt parser 扫描地址历史交易，生成结构化记录并支持导出。

### Riso（PM / Pitch）

1. **自然语言 Swap 确认助手（当前 Mini Demo 主线）**  
   目标用户：第一次尝试 Monad DeFi 的链上新手。  
   痛点：用 AI Agent 表达「把 100 USDC 换成 MON」后，看不懂 Capability 交易树和 Receipt/Changes，不敢签或误签。  
   解决方式：自然语言 → Moss Capability 树 + simulate → 可理解的确认页 → 用户自己签名。

2. **AI Agent 可信交易评分卡**  
   目标用户：轻度使用 AI Agent 的钱包用户。  
   痛点：面对 Agent 返回的多步交易，不知道风险等级和哪些步骤可以信任。  
   解决方式：基于 simulate 结果自动生成风险标签（授权额度、价格影响、MEV 风险），以卡片形式展示。

### eleven（UI / 视觉）

1. **三屏极简 Swap Demo（聚焦确认页可读性）**  
   目标用户：链上新手。  
   痛点：现有 DApp 确认页信息过载，新手不知道哪里该看、哪里该点。  
   解决方式：只保留 3 屏——输入 → Capability/simulate 结果 → 确认，把复杂 effects 视觉化成「付出 / 收到 / 风险」三块。

2. **Moss 交易效果对比卡片**  
   目标用户：想学习 DeFi 的新手。  
   痛点：看不懂同一意图在不同协议/滑点设置下的实际差异。  
   解决方式：用 simulate 同时跑几组参数，用并排卡片展示「原方案 vs 更优方案」。

---

## 三、想法整理与归类

| 归类 | 包含想法 | 目标用户 | 核心问题 | 解决方式 |
|------|----------|----------|----------|----------|
| **A. 交易前解释层** | Neo-1 Receipt Chat、Riso-2 风险评分卡 | 链上新手、轻量用户 | 看不懂交易效果，不敢签 | 用 Moss simulate + Receipt 解析生成人话摘要 / 风险标签 |
| **B. 自然语言 Swap 助手** | Riso-1 主线、eleven-1 三屏 Demo、eleven-2 对比卡片 | Monad DeFi 新手 | Agent 返回 Capability 后仍困惑 | 自然语言 → Capability + simulate → 极简确认页 → 签名 |
| **C. 开发者工具** | Neo-2 Capability 沙盒 | 协议开发者、适配器作者 | 调试 Moss adapter 门槛高 | 可视化 Capability 树 + simulate + Receipt 的沙盒 |
| **D. DAO / 社区工具** | Neo-3 意图信箱 | DAO 运营者、社区成员 | 分发可执行链上操作效率低 | 运营者发布意图卡片，成员一键签名 |
| **E. 历史记录 / 税务** | Neo-4 Receipt 保险柜 | 活跃 DeFi 用户、审计员 | 缺少结构化、可验证的历史记录 | 用 Moss Receipt parser 扫描历史交易并导出 |

---

## 四、筛选讨论

### 评估标准

1. **问题是否真实？** 是否有人真的愿意为看懂交易效果而使用它？
2. **团队是否有能力完成？** 当前三人（Dev + PM + UI）能否在 3–4 天内做出可跑版本？
3. **能否在本周做出可以展示的版本？** 是否能在 Day 5（7/24）前留下 Demo Evidence？

### 逐项评估

| 方向 | 问题真实性 | 团队能力 | 本周可展示性 | 结论 |
|------|-----------|----------|--------------|------|
| A. 交易前解释层 | 高（签名恐惧真实存在） | 高（复用 Mini Demo 链路） | 高 | 与 B 合并 |
| **B. 自然语言 Swap 助手** | **高** | **高** | **高** | **最终选择** |
| C. Capability 沙盒 | 中（解决开发者痛点） | 中（需暴露内部 API） | 中 | 暂放弃 |
| D. DAO 意图信箱 | 中（DAO 场景真实） | 中（需额外合约/后台） | 中 | 暂放弃 |
| E. Receipt 保险柜 | 中（税务/审计需求真实） | 低（需 indexer） | 低 | 暂放弃 |

### 讨论要点

- **B 与 A 的关系**：B 已经包含 A 的核心价值（用 simulate 解释交易效果），且 B 有明确的用户动作（swap）和演示闭环，因此把 A 并入 B，不做单独方向。
- **C 的价值**：团队自身在调试 Capability 时就在经历这个痛点，但沙盒更适合作为 Week 4 Hackathon 的开发者工具方向，本周会让 Demo 失去用户故事冲击力。
- **D 的取舍**：DAO 意图信箱有长期价值，但需要额外写白名单合约和后台发布页，超出本周范围。
- **E 的取舍**：需要 indexer 或遍历区块，本周无法出 Demo Evidence。

---

## 五、最终选择的方向

**自然语言意图 → Moss Capability 树 + simulate → 可理解的确认页 → 用户签名**

具体链路：用户输入「swap 100 USDC to MON on Monad」→ Agent 用预置模板解析意图 → Moss Kuru `swap` Capability 生成未签名交易树 → `simulate` 返回 Receipts / Changes → UI 展示「付出 / 收到 / 滑点 / 授权 / 风险」→ 用户确认后触发钱包签名（至少展示待签名交易，尽量广播）。

---

## 六、选择它的原因

1. **问题真实**：链上新手面对 Agent 返回的 Capability 和授权弹窗普遍存在恐惧，这是团队在前期用户观察中反复看到的场景。
2. **团队能力匹配**：Neo 已本地跑通 Moss Kuru swap + simulate，eleven 可在 3 屏内完成确认页设计，Riso 负责范围控制和用户测试。
3. **本周可展示**：只验证一条 swap 链路，3 分钟 Demo 即可讲完，且能在 Monad 测试网留下交易哈希或合约地址作为证据。
4. **Monad 原生**：低延迟让「说完意图 → 秒级 simulate → 展示结果」的体验成立；EVM 兼容可直接复用 Kuru 协议；Moss 是 Monad 生态原生协议层。
5. **区别于常见方向**：不是又一个通用 AI Agent 或 DeFi 聚合器，而是聚焦「交易效果解释」这一具体信任问题，价值主张清晰。

---

## 七、暂时放弃的想法

| 方向 | 放弃原因 | 后续处理 |
|------|----------|----------|
| Receipt Chat（Neo-1） | 已被最终方向包含，无需单独做 | 作为确认页文案参考 |
| AI Agent 风险评分卡（Riso-2） | 与最终方向合并为「风险区块」 | 在确认页中展示风险标签 |
| Moss Capability 沙盒（Neo-2） | 本周优先用户故事，开发者工具优先级次之 | 列为 Week 4 Hackathon 备选 |
| DAO / 社区意图信箱（Neo-3） | 需要额外合约和后台，超出本周范围 | 列为 Week 4 Hackathon 备选 |
| 链上 Receipt 保险柜（Neo-4） | 需要 indexer，本周不可行 | 列为长期方向，不在本周讨论 |
| 交易效果对比卡片（eleven-2） | 需模拟多组参数，超出 Must Have | 列为 Nice to Have |

---

## 八、下一步行动与负责人

| 行动 | 负责人 | 截止 | 产出 | 依赖 |
|------|--------|------|------|------|
| 将脑暴结论写入团队 Mini Demo 范围与方案设计 | Riso + Neo | 7/22 23:00 | 更新 `mini-demo-scope.md`、`solution-design.md` | 本次会议结论 |
| 搭建前端项目骨架（Vite + React + wagmi） | Neo | 7/23 12:00 | 可运行代码仓库 | 无 |
| 实现意图解析预置模板 | Neo | 7/23 18:00 | 用户输入 → 结构化参数 | 项目骨架 |
| 接入 Moss Kuru swap + simulate | Neo | 7/23 21:00 | 能返回 Capability 树和 Receipt 的 Hook/API | 意图解析 |
| 设计 3 屏主路径线框 / 高保真 | eleven | 7/23 21:00 | 输入屏 → Receipt 屏 → 确认屏 | 无 |
| 准备 3–5 位测试用户与测试问题 | Riso | 7/23 21:00 | 测试者名单 + 反馈表 | 一句话介绍 |
| Day 4 集成确认页 + 用户测试 | Neo + eleven + Riso | 7/24 18:00 | 可签名 Demo + 反馈记录 | simulate Hook 齐 |
| 录制 Demo 视频 + 准备 Pitch | eleven + Riso | 7/25 12:00 | 60–90 秒录屏 + 3 分钟 Pitch | Demo 可运行 |

---

## 九、会议共识

- 本周 Mini Demo 只聚焦 **一条 swap 链路**，不扩展多协议、多链、借贷或 DAO 场景。
- 安全边界：**Moss 只做规划与模拟，不自动签名/广播**；任何资产操作必须有用户明确确认步。
- Demo 必须留下可验证证据：测试网交易哈希 / 合约地址 / 可运行网页 / 录屏，四选一即可。

---

## 关联文档

| 文档 | 路径 |
|------|------|
| 团队介绍 | `submissions/week-03/team.md` |
| 团队组建提交 | `submissions/week-03/team-submission.md` |
| 问题定义 | `submissions/week-03/problem-statement.md` |
| Mini Demo 范围 | `submissions/week-03/mini-demo-scope.md` |
| 团队构建计划 | `submissions/week-03/build-plan.md` |
| Tech 创意卡片 | `submissions/week-03/idea-cards-neo.md` |
