# Week 2｜Challenge｜GitHub Exploration Log — Moss

> 学员：Neo  
> 方向：Dev Builder（Tech）  
> 探索日期：2026-07-14  
> 项目：[nishuzumi/moss](https://github.com/nishuzumi/moss)  
> 本地阅读版本：`0612574f05f46095754d1d3ddd1085c69edf7191`（个人 Fork，**当时为 Plan/expects 时代**）

> ⚠️ **架构勘误（2026-07-20）**  
> 下文目录、Plan、expects、TokenTable、observation 等描述反映探索当日源码，**不是**当前 main 线。  
> 现行框架：Capability tree + exhaustive Receipt（上游 #31）。  
> 请改读：[`moss-architecture-errata.md`](./moss-architecture-errata.md)、[`moss-beginner-guide-v2.md`](./moss-beginner-guide-v2.md)、`experiments/moss/MOSS-STUDY-NOTES.md`。  
> 本日志保留为「当时如何探索仓库」的过程证据，不整体改写。

## 1. 项目简介

Moss 是一个面向 Monad 的 Agent 协议能力层。它把不同 DApp 的 ABI、合约地址、精度换算、授权和清理步骤封装成统一的 `discover → load → action → simulate` 流程，让 AI Agent 使用人类可读参数构建 Plan，再在真实链上状态中模拟并核对实际资金流。

它最重要的边界不是「替 Agent 自动交易」，而是「在签名之前提供可检查的未签名交易与机械验证」。Moss 永不保管私钥、永不签名、永不发送；任何 warning 都应该停止流程，最终决定权仍在用户和钱包。

## 2. README 阅读记录

README 不只介绍功能，还承担了项目的第一层设计说明：

1. **Why**：Agent 自行拼装 calldata 容易在路由、精度、授权、wrap / unwrap、refund 等细节上出错。
2. **Core Flow**：先发现能力，再加载调用契约，由 `action` 生成带量化 `expects` 的 Plan，最后强制 `simulate`。
3. **Safety Boundary**：零 warning 只证明执行结果符合 Plan 的声明，不代表 Plan 一定符合用户原始意图，也不承诺真实成交结果。
4. **Current Scope**：当前面向 Monad 主网，支持 WMON、通用 ERC-20 / ERC-721 与 Kuru；Permit、跨链桥、闪电贷原子组合暂不支持。
5. **Contributor Entry**：协议适配器是主要贡献入口，采用「一个协议一个 package」的结构，并提供 `_template`、参考实现和 Definition of Done。

我的判断：这份 README 同时服务使用者、Agent 集成者和贡献者。它先解释「为什么存在」，再给最短运行路径，最后把深入内容导向 Docs、ADR 与贡献指南，信息层级比较清楚。

## 3. 项目目录结构

```text
moss/
├── .github/
│   ├── ISSUE_TEMPLATE/        # Bug、Feature、Protocol Onboarding 模板
│   ├── workflows/             # CI 工作流
│   └── PULL_REQUEST_TEMPLATE.md
├── docs/
│   ├── README.md              # 文档导航
│   ├── getting-started*.md    # 从运行示例到理解四步流程
│   ├── mcp-tools.md           # 四个 MCP 工具的输入输出契约
│   ├── agent-skill.md         # Agent 必须遵守的安全规则
│   ├── protocol-onboarding.md # 协议适配器开发与提交指南
│   └── adr/                   # ADR 0001–0009，记录架构决策与取舍
├── examples/
│   ├── simple-flow/           # wrap 与 Kuru swap 的最小调用示例
│   └── agent-swap/            # 本地 Monad 主网 fork 上的 Agent 交易闭环
├── packages/
│   ├── core/                  # 装饰器、Registry、Plan、语义类型
│   ├── simulator/             # debug_traceCall、effects 提取、expects 对账
│   ├── erc/                   # 标准 ABI 与地址无关的 ERC 通用行为
│   ├── system/                # Monad runtime、TokenTable、WMON 等链实例
│   ├── protocols/
│   │   ├── _template/         # 新协议适配器模板
│   │   └── kuru/              # Kuru 协议适配器
│   └── mcp-server/            # discover / load / action / simulate 工具入口
├── README.md / README.zh-CN.md
├── CONTRIBUTING.md            # 开发环境、PR 规则、适配器 DoD
├── SECURITY.md                # 安全边界与漏洞报告方式
├── CONTEXT.md                 # 项目统一词汇表
├── package.json
└── pnpm-workspace.yaml        # pnpm Monorepo 配置
```

### 架构理解

依赖方向从「纯机械能力」逐层走向「具体链与协议实例」：

```text
core
├── simulator
├── erc
│   └── system
└── protocols/*
    └── mcp-server
```

这种分层把 ABI、链地址和协议差异限制在应该出现的位置。`core` 不知道具体链上地址；`system` 才保存 Monad 实例；协议包各自维护 ABI、能力、事件、测试与 manifest；`mcp-server` 明确组装要对 Agent 提供的能力目录。

## 4. Docs 阅读记录

| 文档 | 作用 | 我的发现 |
|------|------|----------|
| `docs/getting-started.zh-CN.md` | 从零跑通并拆解完整流程 | 采用「先运行，再逐层打开」的学习顺序，降低复杂系统的理解门槛 |
| `docs/mcp-tools.md` | 定义四个 MCP 工具的契约 | MCP Server 是无状态的，`action` 生成的 Plan 自包含，`simulate` 会重算 `planHash` |
| `docs/agent-skill.md` | 约束 Agent 行为 | 强制模拟、warning 即停、效果与用户意图再次对齐，都是硬规则 |
| `docs/protocol-onboarding.md` | 指导新增协议适配器 | ABI 来源、地址验证、量化 expects、Event receipt、零 warning e2e 都是审查门槛 |
| `docs/adr/` | 记录架构决策 | Maintainer 不只记录「怎么做」，还记录「为什么这样做」与被放弃的方案 |
| `CONTRIBUTING.md` | 统一贡献流程 | PR 需说明动机、改动和测试证据；用户可见改动需 changeset；CI 必须全通过 |

## 5. GitHub 各模块的作用

> 以下状态于 2026-07-14 通过 GitHub 页面与 `gh` API 核验。

### Code / README

- `Code` 是源码、文档、模板和示例的统一入口。
- README 提供项目定位、风险边界、快速开始、目录说明与贡献入口。
- Monorepo 的 package 边界与架构边界基本一致，目录本身就在表达设计。

### Docs

- Docs 不只是 API 手册，还包括新手路径、Agent 规则、协议接入流程和 ADR。
- ADR 让后来的贡献者先理解已有取舍，避免在 PR 中重复争论基础设计。

### Issues

- 当前有 13 个 Open Issue。
- Maintainer 用标签同时表达**工作类型**与**进入难度**，例如：`adapter`、`interface-layer`、`dex`、`lending`、`difficulty:starter`、`difficulty:advanced`、`needs-design`。
- Issue 不只是报错列表，也承担 Roadmap 和设计讨论入口。例如 #13 明确指出 ERC-4626 在写代码前需要先解决实例化方式与 `expects` 表达。

### Pull Requests

- 当前有 2 个 Open PR。
- PR 模板要求说明 What & Why、改动类型、检查清单和验证证据。
- Maintainer 会检查提交历史是否干净。PR #17 虽然目标只是补充新手文档，但分支混入了上游历史，Maintainer 要求先 rebase；这说明「改动内容正确」之外，PR 的可审查性也很重要。
- PR #19 从 Issue #18 出发，只增加 `.gitattributes` 修复 Windows CRLF 问题，附带复现数据、测试证据、CI 成功结果，并触发 Codex Review，展示了完整的 Issue → Fix → CI → Review 链路。

### Discussions

- 仓库当前**未启用 GitHub Discussions**，因此没有可浏览的 Discussion 内容。
- 现阶段需求、设计问题和贡献沟通主要发生在 Issues 与 Pull Requests 中。这个结果本身也是探索发现，不能因为任务模板列出 Discussions 就假设项目一定启用了它。

### Actions / CI

- `.github/workflows/` 管理自动化验证。
- 贡献指南要求 lint、build、typecheck、tests 全部通过；协议能力还要提供 Monad 主网状态上的零 warning e2e 模拟证据。
- PR #19 的 CI 已成功，说明 Maintainer 把机器验证作为合并前的基本门槛。

## 6. 我感兴趣的 Issue：#13 ERC-4626 Tokenized Vaults

- 链接：[Issue #13 — Interface layer: ERC-4626 tokenized vaults](https://github.com/nishuzumi/moss/issues/13)
- 状态：Open
- 标签：`interface-layer`、`difficulty:advanced`、`needs-design`

### 为什么感兴趣

我已经在个人 Fork 中实现过一个可编译、可测试的 MockVault 协议适配器草稿，所以 ERC-4626 是能与现有 Proof of Work 直接衔接的方向。但 Issue #13 让我意识到：做一个固定地址的 Demo Adapter，与为整个 Moss 设计可复用的 ERC-4626 Interface Layer，是两个不同难度的问题。

### Issue 真正要解决的设计问题

1. 使用调用时传入的通用 `vault` 地址，还是在 manifest 阶段实例化每个已审核 Vault？
2. 是否由协议 package 维护经过验证的 Vault Catalog？
3. ERC-4626 的 `deposit / mint / withdraw / redeem` 应如何映射到用户视角的 `supply / withdraw` verb？
4. 资产与 share 的兑换关系如何进入量化 `expects`，才能让模拟器准确检查最小流入与最大流出？
5. 标准 ABI 可以先独立落地，但通用行为仍需要 ADR 级设计结论。

### 如果继续贡献，我会这样推进

1. 先阅读 ADR 0009，并在 Issue 中提出三种实例化方式的比较，而不是直接提交大段代码。
2. 把 `IERC4626.sol → ERC4626Abi` 的编译来源链作为可独立审查的小改动。
3. 用现有 MockVault 草稿验证 `deposit` 和 `withdraw` 的 Plan / expects 形状。
4. 增加 discover / load、Plan shape、share conversion 与 warning 场景测试。
5. 设计结论确定后，再接入真实 Monad Vault，并补充地址来源、主网模拟与零 warning 证据。

## 7. 补充关注的 PR：#19 跨平台换行修复

- 链接：[PR #19 — fix: preserve LF line endings across checkouts](https://github.com/nishuzumi/moss/pull/19)
- 关联：[Issue #18](https://github.com/nishuzumi/moss/issues/18)

这个 PR 的代码改动只有一个 `.gitattributes` 文件，但提交质量很高：它定位到 Windows `core.autocrlf=true` 导致生成文件与 ABI provenance 测试按字节比较失败，给出修复前的 CRLF 数量、修复后的测试结果，并保持原有严格断言不降级。它提醒我，好的开源修复不是「让测试别报错」，而是保留安全约束，同时消除真正的跨平台不确定性。

## 8. 我对 Maintainer 管理方式的理解

1. **README 管入口**：先让用户理解价值与风险，再导向具体文档。
2. **Docs 管知识**：操作指南负责「怎么做」，ADR 负责「为什么这样做」。
3. **Issue 管工作队列**：用类型、领域、难度和设计状态标签降低认领成本。
4. **Template 管信息质量**：Issue / PR 模板要求贡献者提供可复现信息。
5. **CI 管最低质量线**：格式、构建、类型和测试交给自动化；Maintainer 聚焦设计与边界。
6. **小步提交降低审查成本**：从 PR #17 的 rebase 要求和 PR #19 的单文件修复可以看出，可审查性本身就是贡献质量的一部分。

## 9. 学习收获

### 如何阅读一个真实开源项目

我形成了一条比「从头翻源码」更高效的路径：

```text
README 定位问题
→ Docs 建立概念模型
→ 目录确认架构边界
→ CONTRIBUTING 理解质量门槛
→ Issues 观察 Roadmap 与未决问题
→ PRs 学习真实协作与审查
→ 最后带着问题阅读核心代码
```

### 具体收获

- 项目结构不是简单的文件分类，而是在约束依赖和责任边界。
- `expects` 是 Plan 的安全声明，`simulate` 是对声明的机械验证，用户意图对齐仍需要 Agent / 人类完成。
- 一个合格 Issue 应说明背景、设计问题、参考材料与 Definition of Done，而不只是写一句需求。
- 一个合格 PR 要让 Maintainer 能快速回答：为什么改、改了什么、如何复现、如何证明没有破坏原有约束。
- 「先讨论设计，再写实现」不是拖慢速度；对于 ERC-4626 这类影响公共接口层的功能，它是在避免错误抽象扩散到整个项目。

## 10. 参考资料

- Moss Repository：https://github.com/nishuzumi/moss
- README：https://github.com/nishuzumi/moss/blob/main/README.md
- Documentation Index：https://github.com/nishuzumi/moss/blob/main/docs/README.md
- Getting Started：https://github.com/nishuzumi/moss/blob/main/docs/getting-started.md
- MCP Tools：https://github.com/nishuzumi/moss/blob/main/docs/mcp-tools.md
- Agent Skill Guide：https://github.com/nishuzumi/moss/blob/main/docs/agent-skill.md
- Protocol Onboarding：https://github.com/nishuzumi/moss/blob/main/docs/protocol-onboarding.md
- Contributing：https://github.com/nishuzumi/moss/blob/main/CONTRIBUTING.md
- ADRs：https://github.com/nishuzumi/moss/tree/main/docs/adr
- Issue #13：https://github.com/nishuzumi/moss/issues/13
- Issue #18：https://github.com/nishuzumi/moss/issues/18
- PR #19：https://github.com/nishuzumi/moss/pull/19
