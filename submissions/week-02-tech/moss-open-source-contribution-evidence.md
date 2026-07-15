# Moss Open Source Contribution Evidence

> 学员：Neo
> GitHub：NeoWeb3Nova
> 日期：2026-07-15
> 贡献类型：Core Bug Fix

## 提交链接

- Pull Request：https://github.com/nishuzumi/moss/pull/36
- GitHub 主页：https://github.com/NeoWeb3Nova
- Commit：https://github.com/NeoWeb3Nova/moss/commit/865fa71c5224ccbd401e002c8480c8e64013c2a2
- 分支：`NeoWeb3Nova:fix/unsafe-numeric-uint`
- PR 标题：`fix(core): reject unsafe numeric uint inputs`

## 问题

Moss Core 的 `uint` semantic 接受 JavaScript `number`，并通过 `BigInt(value)` 转换为链上整数。超过 `Number.MAX_SAFE_INTEGER` 的数字不能保证被 JavaScript 唯一、精确表示；调用方写出的整数可能在进入 Moss 前已经舍入。如果 Core 继续接受该值，最终 calldata 可能携带另一个整数，例如错误的 ERC-721 token ID。

TDD RED 阶段真实观察到：

```text
promise resolved "{ id: 9007199254740992n }" instead of rejecting
```

## 修复范围

PR 仅包含 3 个文件：

- `.changeset/safe-uint-inputs.md`
- `packages/core/src/semantics.ts`
- `packages/core/test/core-unit.test.ts`

核心行为：

- safe integer number 继续接受；
- unsafe integer number 在 `BigInt` 转换前拒绝；
- 错误信息提示大整数改用十进制字符串；
- 任意精度十进制字符串继续精确转换；
- 负数和小数继续拒绝；
- JSDoc 明确 numeric input 的安全整数边界。

非范围：token amount 浮点策略、Registry、Adapter、文档重构及其他顺手修复。

## TDD 与 Review

1. 先添加回归测试并运行，确认当前实现错误接受 unsafe number。
2. 再添加 `Number.isInteger` 与 `Number.isSafeInteger` 最小 guard。
3. focused test 进入 GREEN，随后运行 Core 和 workspace 全量测试。
4. 独立代码 Review 结论为 **READY**，无 Critical / Important。
5. 采纳唯一 Minor 建议：增加 `uint128` 最大值 `340282366920938463463374607431768211455` 的十进制字符串精确转换测试。

## 本地验证

以下命令均真实执行并以 exit code 0 完成：

```bash
pnpm changeset status
pnpm lint
pnpm -r build
pnpm -r typecheck
MOSS_SKIP_E2E=1 pnpm -r test
NODE_USE_ENV_PROXY=1 pnpm -r test
git diff --check
```

关键结果：

- Biome：84 个文件，无问题；
- Core：2 个测试文件、23 个测试全部通过；
- 离线 workspace 测试通过；
- Monad mainnet e2e 通过，包括 simulator、ERC-20、ERC-721、WMON、Kuru 和 MCP Server；
- changeset 为 `@themoss/core` patch；仓库 linked 配置会联动计算关联包 patch 版本；
- 本地与 Fork 远端 commit SHA 均为 `865fa71c5224ccbd401e002c8480c8e64013c2a2`。

## GitHub CI 与 Review 状态

- Actions run：https://github.com/nishuzumi/moss/actions/runs/29403921889
- 当前状态：`Action required`
- GitHub 页面说明：`This workflow is awaiting approval from a maintainer in #36.`
- 当前 jobs：0；工作流尚未真正执行，因此不能声明 CI 已通过或失败。
- Maintainer Review：尚未发生。
- Merge：尚未发生。

## 上游迁移风险

Maintainer 的 Draft PR #31 正在重写 Core，并将旧 `uint` semantic 替换为 string-only `UnsignedIntegerString` schema。因此 PR #36 是对当前稳定 `main` 的窄范围安全修复。PR 正文已主动披露：如果 #31 先合并，#36 可以被视为 superseded。

这项风险不影响本次 Proof of Work 的真实性，但会影响最终合并概率。对开源贡献而言，如实说明上游冲突比隐藏风险更重要。

## 下一步

- 等待 Maintainer 批准 GitHub Actions；
- 工作流启动后核验每个 check；
- 回应 Review，并按 Maintainer 意见调整；
- Review 或 Merge 发生后补充对应链接，不提前声明结果。
