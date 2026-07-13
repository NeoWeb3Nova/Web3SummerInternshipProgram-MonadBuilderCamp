# Week 2 Day 2｜AI-assisted Dev Plan — Dev Builder（Moss 强化版）

> 学员：Neo  
> 方向：Dev Builder（Tech）  
> 日期：2026-07-14  
> 今日任务：任务 15｜定义一个最小 Web3 原型，说明用户动作、技术组件、要读的文档、真实实现 / mock / 本周不做的边界。

---

## 1. 背景：为什么选择 Moss

本周实习计划强调知识储备与挑战。在研究了 [nishuzumi/moss](https://github.com/nishuzumi/moss) 后，决定以 Moss 作为 Week 2 的主要学习/贡献对象，理由：

1. **Monad-native**：Moss 是为 Monad 设计的 Agent × DeFi 交互层，与本课程的 Monad Builder 方向高度契合。
2. **Agent 协议真实场景**：它解决的是 AI Agent 如何安全地调用链上协议——这正是 Week 3 组队可能深入的方向。
3. **可贡献开源**：Moss 的协议适配器（Protocol Adapter）采用模板化设计，是 Dev Builder 可以落地的明确贡献入口。
4. **与 PactGuard 可组合**：Moss 负责 `discover → load → action → simulate`，PactGuard 负责签名前的预算/白名单/频率检查，两者可构成完整的 Agent 交易安全栈。

---

## 2. 项目一句话

**在本地跑通 Moss 仓库，完成 `discover → load → action → simulate` 完整流程，并产出一份可复用的协议适配器贡献模板/文档改进 PR。**

> 原先的“MonadTally 计数器 Demo”替换为 Moss 深度学习 + 实际开源贡献准备，以匹配实习计划的强度。

---

## 3. 用户/开发者动作

| 动作 | 输入 | 结果 |
|------|------|------|
| 克隆与构建 | `git clone moss` + `pnpm install` + `pnpm -r build` | 本地可运行的 Moss 仓库 |
| 跑通示例 | `pnpm --filter @themoss/example-simple-flow exec tsx src/wmon-wrap.ts` | 完成 discover/load/action/simulate 闭环，无 warnings |
| 阅读核心模块 | `packages/core`、`packages/simulator`、`packages/protocols/_template` | 理解 Plan、expects、simulate 的安全设计 |
| 试写适配器 | 复制 `_template`，填充一个简单的读取或转账能力 | 一个可编译通过的适配器草稿 |
| 贡献准备 | 根据学习体会，提交文档改进 PR 或 Issue | 一份真实的开源贡献证据 |

---

## 4. 技术架构

```
┌─────────────────────────────────────┐
│        Moss Repository (Local Clone)        │
│  ┌────────────┐  ┌─────────────┐  ┌─────────────┐ │
│  │ @themoss/core │  │ @themoss/simulator │  │ protocol adapter │ │
│  │ (装饰器/Plan)  │  │ (debug_traceCall) │  │ (_template)      │ │
│  └────┬─────┘  └───────┬──────┘  └───────┬──────┘ │
│       │                │                    │                  │
│       └─────────────────┬─────────────────┘                  │
│                        │                                       │
│       ┌─────────────────────────────────────┐         │
│       │ @themoss/mcp-server (4 tools: discover/load/action/simulate) │         │
│       └─────────────────────────────────────┘         │
└─────────────────────────────────────┘
                           │
                           ▼
                Monad Mainnet RPC (simulation only)
```

---

## 5. 技术组件清单

| 层级 | 组件 | 状态 | 说明 |
|------|------|------|------|
| 运行环境 | Node ≥ 22 + pnpm | ✅ 已就绪 | 本机 Node 22.22.2, pnpm 11.1.1 |
| 代码库 | `nishuzumi/moss` clone | ✅ 已完成 | 位于 `experiments/moss/` |
| 构建 | `pnpm -r build` | ✅ 已通过 | 全部 package build success |
| 测试 | `MOSS_SKIP_E2E=1 pnpm -r test` | ✅ 已通过 | 12 passed, 7 skipped |
| 示例验证 | `wmon-wrap.ts` | ✅ 已跑通 | discover/load/action/simulate 无 warnings |
| 核心阅读 | core / simulator / _template | 🟡 进行中 | 本周重点 |
| 适配器草稿 | 基于 `_template` 的一个能力 | ⏳ 本周实现 | 可编译即可，不强求 PR 合并 |
| 开源贡献 | 文档 PR / Issue / Demo | ⏳ 尽力而为 | 作为 Bonus 积分 |
| 签名发交易 | 真实钱包调用 | ❌ 本周不做 | Moss 设计原则不允许此行为 |
| 新协议完整适配 | 如 Uniswap / Aave | ❌ 本周不做 | 需要大量 ABI/测试/状态跟踪 |
| 自定义 MCP Server | 扩展工具 | ❌ 本周不做 | 先用现有 server |

---

## 6. 要读的文档（按优先级）

| 优先级 | 文档 | 用途 |
|-------|------|------|
| P0 | Moss README / getting-started.md | 整体架构与快速上手 |
| P0 | docs/mcp-tools.md | 四个工具的输入输出契约 |
| P0 | docs/agent-skill.md | Agent 使用 Moss 的安全规则 |
| P0 | packages/protocols/_template/README.md | 适配器开发 checklist |
| P1 | docs/adr/0002-simulation-via-debug-tracecall.md | 为什么用 debug_traceCall |
| P1 | docs/adr/0004-quantified-expects-in-plans.md | Plan 中 expects 的安全设计 |
| P1 | docs/adr/0006-protocol-packages-and-manifests.md | 为什么一个协议一个 package |
| P1 | packages/system/src/wmon.ts | 参考适配器实现 |
| P2 | docs/protocol-onboarding.md | 完整贡献流程 |
| P2 | CONTEXT.md | 项目术语表 |

---

## 7. 真实实现 / Mock / 本周不做

### 7.1 真实实现（必须跑通）

- [x] 克隆 Moss 仓库并安装依赖
- [x] 本地构建通过
- [x] 本地离线测试通过
- [x] 跑通 `wmon-wrap.ts` 示例（live mainnet simulation）
- [ ] 阅读 `_template` 并试写一个简单适配器草稿
- [ ] 整理学习笔记 + 贡献准备

### 7.2 Mock / Fallback

- 如果 live RPC `debug_traceCall` 受限：切换到 `rpc4.monad.xyz` 或 `monad-rpc.huginn.tech`。
- 如果无法上网：使用 `MOSS_SKIP_E2E=1` 跑离线测试保持进度。
- 适配器草稿可以只实现一个简单 query（如 `balanceOf`），不强求完整 capability。

### 7.3 本周不做

- 不签名、不发送任何交易（这也是 Moss 的设计原则）。
- 不完整实现一个新协议（如 Uniswap/Aave），因需要大量状态跟踪和测试。
- 不写自定义 MCP server，先使用现有 `moss-mcp`。
- 不做移动端 UI、不做 Demo 录屏（保留给 Week 3）。

---

## 8. AI 与人工分工

| 任务 | AI 负责 | 人类负责 |
|------|--------|---------|
| 仓库构建 | 辅助解读构建错误 | 执行 install/build/test |
| 文档阅读 | 摘要 ADR / 核心概念 | 验证理解并形成自己的语言 |
| 示例调试 | 解释错误信息、提供排查步骤 | 执行并验证输出 |
| 适配器草稿 | 基于 `_template` 生成初版 | review 语义正确性、风险声明 |
| 贡献 PR | 起草 PR 描述 | 确认事实、审阅格式、提交 |
| RPC/环境配置 | 提供备选 | 最终选择并验证 |

---

## 9. 验收标准

- [x] `pnpm install` 成功
- [x] `pnpm -r build` 成功
- [x] `MOSS_SKIP_E2E=1 pnpm -r test` 通过
- [x] `wmon-wrap.ts` 跑通并输出 "No warnings"
- [ ] 阅读完 `_template` 和 `wmon.ts`
- [ ] 产出一份学习笔记 / 贡献准备
- [ ] 更新 Role Log 与 AI Collaboration Log Day 2 记录

---

## 10. 与 Week 3 的衔接

| Week 2 产出 | Week 3 可用于 |
|------------|-------------|
| Moss 本地跑通 + 示例验证 | 团队可直接使用或扩展 Moss 做 Agent 交易 Demo |
| 适配器模板理解 | 可以承接新协议适配器开发任务 |
| simulate 安全模型理解 | 与 PactGuard 的签名前检查组成双层安全门 |
| 学习笔记 | 作为团队技术调研和贡献证据 |

---

## 9642; 附录：本地验证记录

```bash
# 克隆与构建
$ git clone https://github.com/nishuzumi/moss.git experiments/moss
$ cd experiments/moss
$ pnpm install
$ pnpm -r build
$ MOSS_SKIP_E2E=1 pnpm -r test

# 跑通示例（live mainnet simulation, 零资金）
$ pnpm --filter @themoss/example-simple-flow exec tsx src/wmon-wrap.ts
# 输出: ✓ No warnings — the unsigned txs may be handed to a wallet for review.
```
