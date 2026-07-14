# Week 2｜Challenge｜Moss Open Source Contribution Plan

> 学员：Neo
>
> Builder 身份：Dev Builder（Tech）
>
> 计划周期：2026-07-14 ～ 2026-07-19
>
> 目标项目：[nishuzumi/moss](https://github.com/nishuzumi/moss)
>
> 对应议题：[Issue #13 — Interface layer: ERC-4626 tokenized vaults](https://github.com/nishuzumi/moss/issues/13)

## 一、贡献方向

我选择 **Dev Builder｜ERC-4626 Interface Layer 基础能力**，以 Issue #13 为上游入口。本周不直接承诺完成整个通用 ERC-4626 Adapter，而是先完成 Maintainer 已明确可以独立落地的第一阶段：

```text
IERC4626.sol → 编译生成 ERC4626Abi → @mossxyz/erc 导出 → 测试与文档 → Draft PR
```

现有 MockVault Adapter 草稿作为本地验证夹具，用来验证 `deposit / withdraw`、Plan 和量化 `expects` 的形状；只有在 Issue 设计讨论明确后，才把通用行为推进到正式上游实现。

## 二、为什么选择它

1. **与我的 Builder 身份匹配**：我走 Dev / Tech 路线，能够完成 TypeScript、Solidity ABI、测试、Monorepo 构建与 PR 验证。
2. **能复用已有 Proof of Work**：我已经阅读 Moss 的 `core`、`simulator`、`erc`、`_template` 和 `wmon.ts`，并实现过可编译、可测试的 MockVault Adapter 草稿，不需要从零熟悉项目。
3. **是真实上游需求**：Issue #13 由 Maintainer 创建，ERC-4626 是 Morpho MetaMorpho、Euler EVK Vault 等收益协议的共同基础，贡献具备复用价值。
4. **范围可控、便于审查**：完整 ERC-4626 抽象仍有实例化方式、verb 映射和 share / asset `expects` 等设计问题；先提交 ABI 基础，可以避免在设计未定时制造过大的 PR。
5. **贡献质量可验证**：产出可以通过源码生成链、单元测试、构建、类型检查、Lint、CI 与 Draft PR 形成完整证据链。

## 三、本周目标

### 必须完成（Minimum）

- [ ] 在 Issue #13 下确认首个 PR 的边界，避免与其他贡献者重复开发。
- [ ] 按 ADR 0007 建立 `IERC4626.sol → ERC4626Abi` 的可追溯编译生成链，不手写 ABI。
- [ ] 在 `@mossxyz/erc` 中导出 `ERC4626Abi`，保持接口层无 Monad 地址、无协议实例数据。
- [ ] 增加 ABI provenance、关键函数/事件与导出稳定性的测试。
- [ ] 补充必要文档和 changeset，说明动机、改动范围与验证方式。
- [ ] 运行项目质量门：build → typecheck → lint → offline tests，并保存真实输出。
- [ ] 提交一个边界清晰、提交历史干净的 Draft PR。

### 可选扩展（Stretch）

- [ ] 用现有 MockVault 验证 `deposit / withdraw` 的 Plan 与量化 `expects`。
- [ ] 将三种实例化方案的取舍整理成 Issue 设计回复：调用时传地址、manifest-time instantiation、协议包维护 Vault Catalog。
- [ ] Maintainer 确认方向后，再为通用 ERC-4626 行为补充最小实现或后续 Issue。

### 本周明确不做

- 不直接接入 Morpho、Euler 等完整协议。
- 不在 `@mossxyz/erc` 写入任何具体 Vault 地址。
- 不在设计未确认前同时实现 `deposit / mint / withdraw / redeem` 全部抽象。
- 不放宽测试或跳过 ABI 来源、量化 `expects`、Event confirmation 等安全约束。
- 不触碰签名、私钥和交易发送；Moss 仍只构建与模拟。

## 四、预计产出

| 产出 | 形式 | 完成证据 |
|---|---|---|
| Scope 对齐 | Issue #13 设计回复 | Maintainer 可见的评论链接 |
| ABI 基础实现 | 小范围 Git 分支与 commits | `IERC4626.sol`、生成脚本、`ERC4626Abi` 导出 |
| 自动化测试 | Vitest / provenance tests | 测试命令与通过数量 |
| 质量验证 | build / typecheck / lint / tests | 终端日志或 CI checks |
| 上游贡献 | Draft Pull Request | PR 链接、清晰的 What / Why / Evidence |
| 技术记录 | Markdown 技术笔记 | 设计取舍、失败记录、人工判断与下一步 |
| 本地验证 | MockVault 对照实验（可选） | Plan / expects 输出与测试结果 |

> 本周成功标准不是“PR 必须被合并”，而是形成一份 **范围已对齐、实现可复现、测试可验证、Maintainer 容易审查** 的真实贡献。

## 五、完成计划

| 日期 | 工作重点 | 当日可检查结果 |
|---|---|---|
| 07-14（周二） | 确定 Issue #13 与最小 PR 范围 | Contribution Plan、Scope 清单 |
| 07-15（周三） | 阅读 ADR 0007 / 0009，确认 ABI 生成方式并在 Issue 对齐 | Issue 回复、实现分支 |
| 07-16（周四） | 实现 IERC4626 编译链、ABI 导出与 focused tests | 小步 commits、focused tests |
| 07-17（周五） | 用 MockVault 验证接口形状，补文档与 changeset | Plan / expects 记录、文档 diff |
| 07-18（周六） | 运行全套质量门，自审 diff 与提交历史 | build / typecheck / lint / test 日志 |
| 07-19（周日） | 提交 Draft PR，回应 Review 并整理复盘 | PR 链接、最终技术笔记 |

## 六、风险与应对

| 风险 | 应对 |
|---|---|
| Issue 已被其他贡献者认领或实现重叠 | 写代码前先在 Issue 对齐，必要时缩小为测试、文档或独立 ABI PR |
| 通用行为设计尚未确定 | 把 ABI 基础与通用 Adapter 分成两个阶段，首个 PR 不越过已确认边界 |
| pnpm / decorator / TypeScript 工具链差异 | 严格遵循 Node ≥ 22、pnpm 11、Vitest 3、TypeScript 5.9 的项目约束 |
| 主网 e2e 或网络不稳定 | 先跑 `MOSS_SKIP_E2E=1` 的离线验证，再单独补真实 mainnet simulate 证据 |
| PR 过大、难以 Review | 保持单一目的、小步 commit、无无关重构；PR 中明确 What / Why / Evidence |

## 七、AI 与人工分工

- **AI 协助**：检索相关文件、生成测试骨架、解释错误、整理 diff 与验证日志。
- **人工负责**：确认贡献范围、判断架构边界、核验 ABI 来源、运行测试、审查安全语义、撰写 Issue / PR 沟通。
- **底线**：AI 生成内容不能直接提交；每个 ABI、地址、测试结果和设计结论都必须人工核验。

## 八、参考资料

- Moss Repository：https://github.com/nishuzumi/moss
- Issue #13：https://github.com/nishuzumi/moss/issues/13
- CONTRIBUTING：https://github.com/nishuzumi/moss/blob/main/CONTRIBUTING.md
- Protocol Onboarding：https://github.com/nishuzumi/moss/blob/main/docs/protocol-onboarding.md
- ADR 0007 — ABI Origin：https://github.com/nishuzumi/moss/blob/main/docs/adr/0007-abi-origin.md
- ADR 0009 — ERC Interface Layer：https://github.com/nishuzumi/moss/blob/main/docs/adr/0009-erc-interface-layer-and-composition.md
- 既有学习笔记：`experiments/moss/MOSS-STUDY-NOTES.md`
- 既有 MockVault 草稿：`experiments/moss/packages/protocols/mockvault/`
