# Week 2｜Challenge｜认识一个开源项目：Moss

> 学员：Neo  
> GitHub 用户：NeoWeb3Nova  
> 日期：2026-07-14  
> 项目方向：Dev Builder（Tech）

## 提交材料

### 1. GitHub 用户主页

https://github.com/NeoWeb3Nova

### 2. 已 Star Moss 的证明

![NeoWeb3Nova 已 Star nishuzumi/moss](./moss-star-proof.png)

公开 Star 记录：

https://github.com/NeoWeb3Nova?tab=stars

### 3. 100～200 字分享

> Moss 把 Monad 上复杂的协议交互封装成 discover → load → action → simulate 的统一能力，让 AI Agent 不必自行拼装 ABI、地址和 calldata。它先生成未签名交易，再基于真实链上状态模拟并核对资金流，出现异常就停止，把最终签名权留给用户。我认为它未来可用于 DeFi 交易助手、自动化金库、DAO 财库和跨协议策略执行，成为 Agent 与钱包之间的安全执行层。

正文共 111 个汉字，符合 100～200 字要求。

### 4. Moss 开源贡献 PR

- PR：[`fix(core): reject unsafe numeric uint inputs`](https://github.com/nishuzumi/moss/pull/36)
- GitHub 主页：https://github.com/NeoWeb3Nova
- Commit：[`865fa71`](https://github.com/NeoWeb3Nova/moss/commit/865fa71c5224ccbd401e002c8480c8e64013c2a2)
- 分支：`NeoWeb3Nova:fix/unsafe-numeric-uint`
- 贡献类型：Core Bug Fix + Regression Tests + Changeset
- 完整证据：[`moss-open-source-contribution-evidence.md`](./moss-open-source-contribution-evidence.md)
- 当前状态：PR 已提交；GitHub Actions 正等待 Maintainer 批准运行，尚未收到 Review 或 Merge。

---

## 项目简介

Moss 是一个面向 Monad 的 AI Agent 链上协议交互框架。它把不同 DApp 和协议的复杂调用统一为可发现、可加载、可执行、可模拟的能力，让 Agent 使用人类可读参数生成未签名交易，而不是直接处理 ABI、合约地址、calldata、代币精度及多步骤清理逻辑。

## 核心问题

AI Agent 能理解用户意图，却不适合临时拼装高风险链上交易。一次看似简单的 Swap 可能涉及 Router 地址、代币包装、授权额度、滑点、退款和多笔调用；只要其中一项“几乎正确但不完全正确”，就可能造成资产损失。同时，交易正确执行了自身声明的动作，也不代表它符合用户原始意图。

## 核心能力

1. **discover**：按用户视角的动作查找协议能力，例如 swap、wrap、transfer。
2. **load**：读取能力的参数语义、意图模板和风险标签。
3. **action**：由协议适配器生成 Plan，包括未签名交易、预期资金流和完整性哈希。
4. **simulate**：基于 Monad 真实链上状态回放交易，将实际效果与 Plan 的 `expects` 对账。
5. **安全停机**：发现未声明资金流、超额授权、Plan 篡改或交易回滚等 warning 时停止。
6. **签名隔离**：Moss 只构建和验证交易，永不签名、永不发送，私钥始终留在钱包端。

## 可能应用场景

- DeFi 交易助手：在 Swap、Wrap、转账前自动生成并验证交易。
- 自动化金库：执行再平衡、收益领取和资产配置前检查资金流与授权。
- DAO 财库：为提案执行生成可审计、可模拟的交易计划。
- 跨协议策略：验证 claim → swap → supply 等多步骤链上流程。
- Agent Wallet 安全层：作为 AI Agent 与钱包签名器之间的交易验证网关。
- 协议接入市场：通过标准化 Adapter 让更多 Monad 协议被 Agent 安全调用。

## 我的理解

Moss 的关键价值不是“让 Agent 更方便地发交易”，而是把 Agent 从不可靠的交易拼装者，降级为受约束的意图协调者。协议适配器负责正确构建，模拟器负责机械对账，Agent 负责检查结果是否符合用户原意，钱包和用户保留最终签名权。这种职责分离比单纯增加 Prompt 规则更可靠，也更适合承载真实资产。

## 参考链接

- Moss GitHub：https://github.com/nishuzumi/moss
- README：https://github.com/nishuzumi/moss/blob/main/README.md
- Getting Started：https://github.com/nishuzumi/moss/blob/main/docs/getting-started.md
- MCP Tools：https://github.com/nishuzumi/moss/blob/main/docs/mcp-tools.md
- Agent Skill Guide：https://github.com/nishuzumi/moss/blob/main/docs/agent-skill.md
- 本地深度学习笔记：`experiments/moss/MOSS-STUDY-NOTES.md`
