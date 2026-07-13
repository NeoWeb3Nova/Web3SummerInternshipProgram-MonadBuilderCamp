# Week 2｜AI Collaboration Log

> 学员：Neo  
> 搭档：Nova001（Hermes Agent）  
> 日期：2026-07-14（Day 1 基础版 + Day 2 Moss 深度版）  
> 对应交付物：
> - `submissions/week-02-tech/role-choice-card.md`
> - `submissions/week-02-tech/week-2-role-log.md`
> - `submissions/week-02-tech/dev-plan.md`
> - `experiments/moss/MOSS-STUDY-NOTES.md`
> - `experiments/moss/packages/protocols/mockvault/`

---

## 本次协作任务

1. Day 1：完成 Week 2 职业方向选择与角色定位。
2. Day 2：深度学习 nishuzumi/moss 项目原理，输出学习笔记，并写出一个简单的 protocol adapter 草稿。

---

## AI 帮了什么

### Day 1

| 环节 | AI 贡献 |
|------|--------|
| 方向梳理 | 根据「开发者」「最小 Demo」「已全面跟 AI 协同」等简短输入整理成结构化文档 |
| 文档生成 | 按任务模板生成 Role Choice Card、Role Log、AI Collaboration Log |
| 内容补全 | 在缺少笔记的情况下，结合 Week 2 任务要求补充合理的参考资料、每日计划和协作反思 |
| 格式规范 | 自动应用中文排版和 Markdown 表格，保持提交物整洁可读 |

### Day 2

| 环节 | AI 贡献 |
|------|--------|
| 项目构建 | 执行 Moss 仓库的 clone、install、build、test，验证环境可用 |
| 示例调试 | 文档中的 `src/play.ts` 不存在时，AI 通过 `find` 定位到实际示例 `src/wmon-wrap.ts`，并跟踪解释输出 |
| 核心模块阅读 | 逐行解读 `packages/core`、`packages/simulator`、`wmon.ts`、`_template`，摘要关键设计思想 |
| 学习笔记 | 将阅读心得整理成 `MOSS-STUDY-NOTES.md`，包括架构、核心类、设计原则、与 PactGuard 的可能组合 |
| 适配器草稿 | 基于 `_template` 生成 `mockvault` package：ABI、adapter、manifest、offline test |
| 错误修复 | 在 `index.ts` 更新导出时纠正了残留的 `ExampleProtocol` 引用，确保 build 通过 |

---

## 人类做了什么（删改 / 核查 / 拍板）

| 环节 | 人类贡献 |
|------|---------|
| 方向拍板 | 明确选择 Dev / Tech，后来决定从“MonadTally 计数器 Demo”改为以 Moss 深度学习为主线 |
| 范围定义 | Day 1 确定最小产出是“Foundry + 前端页面”；Day 2 重新定义为“本地跑通 Moss + 学习笔记 + 适配器草稿” |
| 资料确认 | 确认实际查看的链接和文档（Moss README、getting-started、ADR 等） |
| 问题排查 | 当 `src/play.ts` 报错时，人类决定使用 `find` 查看实际文件结构，然后才让 AI 跟进 |
| 原理审查 | 对 AI 摘要的架构、设计思想做了人工检查，确保没有误读或漂移 |
| 适配器边界 | 确定 mockvault 只用于学习，地址是 fake，不会作为真实贡献提交 |
| 最终审核 | 对 AI 生成的学习笔记、adapter 代码、测试做了最终确认 |

---

## 交给 AI 很合适的部分

- 仓库构建、运行测试脚本、格式化输出
- 大段代码/文档的结构化摘要
- 基于模板生成适配器草稿
- 学习笔记的整理与 Markdown 编排
- 错误信息的初步解释和排查建议

---

## 不能交给 AI 的部分

- **方向与范围决策**：是否从计数器 Demo 改为 Moss 深度学习，由人类拍板。
- **贡献真实性**：mockvault 的地址是 fake，不能作为真实贡献提交；真正的 PR 必须有真实合约验证。
- **安全边界**：Moss 设计原则是“永远不签名”，任何让 AI 跳过 simulate 或诱导签名的情况必须拒绝。
- **链上状态验证**：AI 可以解释 simulate 输出，但真实交易 hash、合约地址必须由人类通过浏览器/节点验证。
- **意图对齐**：simulate 无 warning 只代表 Plan 做了它声明的事，是否符合用户原意需要人类最终判断。
- **私钥/助记词**：AI 不接触，任何签名动作由人类在本地钱包完成。

---

## 人机分工对照表（Day 2 Moss 学习）

| 任务环节 | AI 职责 | 人类职责 |
|---------|--------|---------|
| 仓库构建 | 执行 install/build/test | 确认环境、检查输出 |
| 示例验证 | 解释错误、定位正确文件 | 决定跟进方向 |
| 核心阅读 | 逐行分析并摘要 | 审查理解、提问纠偏 |
| 学习笔记 | 整理为 Markdown | 审阅并确认准确 |
| 适配器草稿 | 基于模板生成 | 确认边界（fake 地址，仅用于学习） |
| 测试 | 运行并报告结果 | 确认测试通过 |

---

## 协作模式总结

> **AI 是解读和整理层，人类是方向和安全边界层。**
>
> 在 Moss 这种高风险领域，AI 可以帮助快速理解代码结构和生成学习笔记，但“是否签名”“是否可以作为真实贡献”“是否符合设计原则”必须由人类把关。

---

## 改进点

- 下次先自己写一份关键词/bullet list，再让 AI 扩写成完整文档，减少 AI 对事实的推测。
- 在深度阅读时，可以先让 AI 列出问题清单，人类逐个确认后再让 AI 回答，提高理解深度。
- 对于贡献级的 adapter，人类应该先确定真实协议和合约地址，再让 AI 帮助填充代码。
