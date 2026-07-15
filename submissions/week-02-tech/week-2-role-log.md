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
| Moss GitHub Issues / Pull Requests | 开源协作 | 理解 Maintainer 如何用标签、模板、CI 和 Review 管理贡献 |
| Issue #13：ERC-4626 tokenized vaults | 设计议题 | 认识到通用接口层需要先解决实例化方式、verb 与 share / asset expects |
| PR #19：preserve LF line endings | Bugfix / PR | 学到应保留严格测试约束并消除跨平台根因，而不是放宽断言 |

#### 使用过的 Prompt（示例）

> 「我是 Dev 方向，本周想深入学习并贡献 nishuzumi/moss。请帮我定义一个最小 Scope，包括本地构建、示例验证、核心模块阅读、适配器草稿、贡献准备，并明确本周不做的边界。」

> 「基于 Moss 的 README、Docs、Issues、Pull Requests 和目录结构，整理一份 GitHub Exploration Log，并区分已经核验的事实、个人判断与下一步贡献设想。」

#### 遇到的问题 / 错误

- 问题：按文档运行 `pnpm --filter @themoss/example-simple-flow exec tsx src/play.ts` 报错，因为 `src/play.ts` 不存在。
- 解决：通过 `find` 查找实际示例文件，改用 `src/wmon-wrap.ts` 成功跑通。
- 发现：任务要求查看 Discussions，但 Moss 当前未启用该模块；日志中如实记录「未启用」，不虚构讨论内容。
- 协作观察：PR #17 因分支混入上游提交被 Maintainer 要求 rebase，说明提交历史整洁也是贡献质量的一部分。

#### 判断变化

- 决定放弃原先的“MonadTally 计数器 Demo”，转攻 **Moss 深度学习 + 开源贡献准备**。
- 认为 Week 2 最有价值的产出是**能跑通一套现代 Agent 交易安全层，并理解其可贡献点**。

#### 今日产出

- 本地跑通 Moss：`pnpm install` / `pnpm -r build` / `MOSS_SKIP_E2E=1 pnpm -r test` 通过
- 验证示例 `wmon-wrap.ts` 输出 `✓ No warnings`
- 重写 `submissions/week-02-tech/dev-plan.md` 为 Moss 强化版
- 完成 `submissions/week-02-tech/moss-project-introduction.md`
- 完成 `submissions/week-02-tech/github-exploration-log-moss.md`
- 完成 `submissions/week-02-tech/moss-open-source-contribution-plan.md`
- 生成 Contribution Plan 的 HTML、PNG 与单页 PDF 提交证据包
- 完成 `daily/2026-07-14.md`

#### 下一步计划

- Day 3：在 Issue #13 对齐首个 PR 边界，阅读 ADR 0007 / 0009。
- Day 4：完成 `IERC4626.sol → ERC4626Abi` 编译链、导出与 focused tests。
- Day 5：用 MockVault 做对照验证，补文档、changeset 与质量门证据。
- Day 6：自审 diff 和提交历史，提交 Draft PR。
- Day 7：回应 Review，整理技术笔记与 Week 3 Portfolio Pack。

---

### 2026-07-15（Day 3）｜完成第一个 Moss Core PR

#### 学习内容

| 资料/链接 | 类型 | 收获 |
|-----------|------|------|
| Moss `uint` semantic 与 `decodeParams` | Core 源码 | JavaScript unsafe integer 会在进入 `BigInt` 前丢失调用者原始意图，链上整数参数应在转换前建立安全边界 |
| `Number.isSafeInteger` | JavaScript 数值语义 | `Number.isInteger` 只能证明数值看起来是整数，不能证明它仍可被唯一、精确表示 |
| Changesets linked packages | 发布工程 | 一个 `@themoss/core` patch changeset 会按仓库 linked 配置联动计算其他包的 patch 版本 |
| GitHub 外部 Fork Actions | 开源协作 | 首次外部贡献的 workflow 可能先进入 `action_required`，需要 Maintainer 批准后才真正创建 CI jobs |
| Draft PR #31 | 上游迁移风险 | 新框架把旧 `uint` semantic 替换为 string-only schema；当前 PR 是对稳定 `main` 的窄范围安全修复，并如实披露 supersession 风险 |

#### AI 协作与人工判断

- AI 辅助完成代码检索、风险建模、TDD 用例、质量门执行、PR 正文与独立 Review。
- 人工最终选择 `fix(core): reject unsafe numeric uint inputs` 作为首个 PR 方向，并确认不混入文档、Adapter 或其他顺手修复。
- 独立 Reviewer 给出 READY，无 Critical / Important；采纳唯一 Minor 建议，增加 `uint128` 最大值字符串测试。
- 对 PR #31 的重构风险保持透明，没有把“本地测试通过”描述成“CI 已通过”或“必然会合并”。

#### 今日产出

- 上游 PR：https://github.com/nishuzumi/moss/pull/36
- Commit：`865fa71c5224ccbd401e002c8480c8e64013c2a2`
- 修改范围：Core semantic、Core regression tests、patch changeset，共 3 个文件
- TDD：先观察 unsafe number 被错误接受的 RED，再实现最小 guard 进入 GREEN
- 验证：lint、build、typecheck、离线全量测试、Monad mainnet e2e 全部在本地 exit 0
- GitHub Actions：https://github.com/nishuzumi/moss/actions/runs/29403921889（等待 Maintainer 批准）
- 证据：`submissions/week-02-tech/moss-open-source-contribution-evidence.md`

#### 下一步计划

- 等待 Maintainer 批准 CI，并在工作流实际运行后核验每个 check。
- 及时回应 Review；若 #31 先合并，则接受 PR 被 supersede，并把安全边界经验迁移到新框架贡献。
- 将 Review / Merge 链接补充到证据文件，不提前声明尚未发生的结果。

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
