# Week 2｜Role Log — Dev / Tech

> 方向：Dev Builder（Tech）  
> 学员：Neo  
> 起止日期：2026-07-13 ~ 2026-07-19

---

## 当前目标

完成一个基于 Foundry 管理的、带前端页面的最小 Demo，并产出可验证的交易/部署记录。

---

## 每日记录

### 2026-07-13（Day 1）｜职业方向选择

#### 学习内容

| 资料/链接 | 类型 | 收获 |
|-----------|------|------|
| Week 2 任务说明（当前项目 `tasks/week-02-tech.md`） | 课程任务 | 明确 Tech 方向任务：选择方向、建立 Role Log、完成 AI Collaboration Log |
| Monad X https://x.com/monad | 社区/内容运营 | 了解官方活动预热节奏和 Builder 内容调性 |
| Monad Discord https://docs.monad.xyz/official-links | 社区运营 | 观察用户互动方式、FAQ 和活动组织形式 |
| Farcaster https://warpcast.com/ | Builder 社区 | 观察 Web3 原生讨论氛围和内容传播逻辑 |
| Monad Developer Docs https://docs.monad.xyz/ | 开发文档 | 确认 RPC、Faucet、部署流程和 EVM 兼容性 |

#### 使用过的 Prompt（示例）

> 「我是 Dev 方向，本周要完成一个基于 Foundry 管理、带前端页面的最小 Demo，请帮我梳理合约层和前端层的最小范围。」

> 「帮我对比在 Monad 测试网、Anvil 本地网络和 Sepolia 上部署 Foundry 合约的步骤差异。」

#### 遇到的问题 / 错误

- 暂无技术错误。方向性选择已完成。

#### 判断变化

- 原本犹豫是否要做 Ops（社区观察），但确认自己更擅长代码落地，决定主攻 Tech。
- 最小产出从「单一合约」扩展到「合约 + 前端页面」，因为 Week 3 组队更需要端到端能力。

#### 今日产出

- 本 Role Log 初版
- `submissions/week-02-tech/role-choice-card.md`
- `submissions/week-02-tech/ai-collaboration-log.md`

#### 下一步计划

- Day 2：把职业方向变成可执行 Scope，输出 Dev Plan。
- Day 3：确认 Monad 测试网 RPC 与 Faucet，完成首次部署。
- Day 4：搭建最小前端页面，实现钱包连接与合约读取。
- Day 5：实现前端写入交易，并记录交易哈希。
- Day 6：整理 Demo 文档、截图/录屏，准备 Week 3 组队素材。
- Day 7：复盘 Week 2，更新 Role Log 终版。

---

### 2026-07-14（Day 2）｜把职业方向变成可执行 Scope

#### 学习内容

| 资料/链接 | 类型 | 收获 |
|-----------|------|------|
| Week 2 Day 2 任务说明（当前项目 `tasks/week-02-tech.md`） | 课程任务 | 明确 Day 2 目标：把职业方向变成一个可执行 Scope |
| Moss README + getting-started.md | 协议/工具 | 理解 `discover → load → action → simulate` 四步骤 |
| docs/mcp-tools.md | 工具契约 | 确认 discover/load/action/simulate 的输入输出 |
| docs/agent-skill.md | Agent 安全 | 明确必须 simulate 后才能给用户/签名者 |
| packages/protocols/_template | 贡献入口 | 了解一个 protocol adapter 的最小结构 |

#### 使用过的 Prompt（示例）

> 「我是 Dev 方向，本周想深入学习并贡献 nishuzumi/moss。请帮我定义一个最小 Scope，包括本地构建、示例验证、核心模块阅读、适配器草稿、贡献准备，并明确本周不做的边界。」

#### 遇到的问题 / 错误

- 问题：按文档运行 `pnpm --filter @themoss/example-simple-flow exec tsx src/play.ts` 报错，因为 `src/play.ts` 不存在。
- 解决：通过 `find` 查找实际示例文件，改用 `src/wmon-wrap.ts` 成功跑通。

#### 判断变化

- 决定放弃原先的“MonadTally 计数器 Demo”，转攻 **Moss 深度学习 + 开源贡献准备**。
- 认为 Week 2 最有价值的产出是**能跑通一套现代 Agent 交易安全层，并理解其可贡献点**。

#### 今日产出

- 本地跑通 Moss：`pnpm install` / `pnpm -r build` / `MOSS_SKIP_E2E=1 pnpm -r test` 通过
- 验证示例 `wmon-wrap.ts` 输出 `✓ No warnings`
- 重写 `submissions/week-02-tech/dev-plan.md` 为 Moss 强化版

#### 下一步计划

- Day 2 下午 / Day 3：逐行阅读 `packages/core`、`packages/simulator`、`_template`、`wmon.ts`。
- Day 3 下午：试写一个简单的 query/capability 草稿。
- Day 4：根据学习体会，确定一个可贡献的文档/测试/adapter 改进点。
- Day 5：整理 Portfolio Pack 与 Week 3 Role Statement。

---

## 汇总资源索引

| 资源 | 链接 | 用途 |
|------|------|------|
| Monad Developer Docs | https://docs.monad.xyz/ | 开发、部署、RPC |
| Foundry Book | https://book.getfoundry.sh/ | 合约编译/测试/部署 |
| Remix IDE | https://remix.ethereum.org/ | 快速验证合约逻辑 |
| Hardhat Docs | https://hardhat.org/docs | 备用工具链 |
| Cursor Docs | https://docs.cursor.com/ | AI Coding 工作流 |
| GitHub Docs | https://docs.github.com/ | 协作流程 |
| viem docs | https://viem.sh/ | 前端链交互 |
| RainbowKit docs | https://www.rainbowkit.com/docs | 钱包连接适配 |

---

> 本文件会持续更新到 Week 2 结束，用于追踪学习材料、Prompt、错误和判断变化。
