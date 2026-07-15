# MOSS Unsafe Numeric Uint 修复设计

## 背景

MOSS Core 的 `uint` semantic type 同时接受十进制字符串和 JavaScript `number`，随后通过 `BigInt(value)` 转换为链上无符号整数。

JavaScript `number` 无法精确表示超出安全整数范围的值。例如，调用方写出的 `9007199254740993` 在进入 `BigInt()` 前已经被舍入为 `9007199254740992`。如果该值用于 ERC-721 token ID，MOSS 可能为错误的 NFT 构建 calldata。

这与 MOSS「由系统负责正确组装交易」的安全目标冲突。

## 目标

阻止 `uint` semantic type 接受无法被 JavaScript `number` 精确表示的整数，同时保留十进制字符串的任意精度输入能力。

建议 PR 标题：

```text
fix(core): reject unsafe numeric uint inputs
```

## 行为设计

`uint.decode(value)` 按以下规则处理输入：

1. 十进制字符串：继续通过 `BigInt(value)` 解析，可表示任意精度的非负整数。
2. JavaScript `number`：仅接受 `Number.isSafeInteger(value)` 为真的非负整数。
3. 超出安全整数范围的 `number`：拒绝，并提示调用方改用十进制字符串。
4. 小数、`NaN`、`Infinity`、负数及其他类型：继续拒绝。

错误信息应明确说明：大整数必须以十进制字符串传入，避免调用方通过重试继续发送不安全的 `number`。

## 修改范围

预计只修改：

- `packages/core/src/semantics.ts`
- `packages/core/test/core-unit.test.ts`
- `.changeset/safe-uint-inputs.md`

如最新上游结构因 PR #31 发生变化，则只迁移到新框架中等价的 semantic type 与测试文件，不扩大功能范围。

## 测试设计

新增回归测试覆盖：

1. 接受安全整数 `number`，例如 `42`。
2. 接受边界值 `Number.MAX_SAFE_INTEGER`。
3. 拒绝超出边界的 numeric input，例如 `Number.MAX_SAFE_INTEGER + 1`。
4. 错误信息要求使用 decimal string。
5. 接受同一大整数的字符串形式，例如 `"9007199254740992"`，并精确转换为对应 bigint。
6. 继续拒绝负数和小数。

测试必须先证明当前实现会接受并静默转换不安全数字，再实施修复。

## 验证

在 MOSS 子仓库执行：

```bash
pnpm lint
pnpm -r build
pnpm -r typecheck
MOSS_SKIP_E2E=1 pnpm -r test
```

如网络与 Monad RPC 可用，再执行完整测试：

```bash
NODE_USE_ENV_PROXY=1 pnpm -r test
```

PR 证据应包含：

- 修复前失败场景或回归测试说明；
- 修复后的 focused test；
- lint、build、typecheck、offline test 输出；
- GitHub Actions CI 状态。

## Git 与 PR 边界

1. 核验并配置官方仓库 `nishuzumi/moss` 为 `upstream`。
2. 从最新 `upstream/main` 创建独立修复分支。
3. 不从当前已分叉的 Fork `main` 直接创建 PR。
4. 不包含现有 Beginner Guide、MockVault、agent-swap demo 或父仓库文件。
5. 只向用户 Fork 推送功能分支，再向 `nishuzumi/moss:main` 创建 PR。

## PR #31 风险

Maintainer 的 Draft PR #31 正在重写 Core semantic types 和测试文件。实施前必须重新核验其状态：

- 若 #31 尚未合并：基于最新 `main` 完成本 PR，并在 PR 描述中保持范围独立；必要时等待或跟随 Maintainer 的 rebase 建议。
- 若 #31 已合并：在新框架的等价位置实现相同行为和测试。

不把 #31 的其他框架迁移内容带入本 PR。

## 非目标

本 PR 不处理：

- `tokenAmount`、`fixedAmount` 或 `nativeAmount` 的一般浮点输入策略；
- `Registry.use()` 的原子性；
- Issue Template 标签；
- Protocol Adapter；
- 无关文档重写或重构。

## 成功标准

- 不安全 numeric uint 被明确拒绝；
- 任意精度十进制字符串仍可精确解析；
- 回归测试覆盖安全边界与错误提示；
- 所有仓库检查通过；
- PR 只包含该安全修复及必要 changeset。
