# Week 2｜Challenge｜为 Moss 新增一个 Protocol Adapter

> 学员：Neo
> GitHub 用户：NeoWeb3Nova
> 日期：2026-07-17
> 项目方向：Dev Builder（Tech）

## 提交材料

### 1. Pull Request 链接

https://github.com/NeoWeb3Nova/moss/pull/1

### 2. GitHub 用户主页

https://github.com/NeoWeb3Nova

### 3. Adapter 名称

`@themoss/protocol-neverland`

### 4. 简要介绍（100 字以内）

> Neverland 是 Monad 主网上的原生 Aave V3 借贷市场。该 Adapter 让 Moss Agent 可以安全地 supply、withdraw 并查询账户健康数据；aToken 地址运行时解析，量化资金流向，并通过 Supply/Withdraw 事件收据确认执行，避免 Agent 硬编码协议状态。

正文共 98 个汉字，符合 100 字以内要求。

## 技术证据

- 本地仓库：`/home/neo/workspace/projects/Web3SummerInternshipProgram-MonadBuilderCamp/experiments/moss`
- 分支：`feat/neverland-adapter`
- 提交：[`3c04384`](https://github.com/NeoWeb3Nova/moss/commit/3c04384)
- 验证结果：
  - `pnpm -r build` 通过
  - `pnpm -r typecheck` 通过
  - `pnpm biome check .` 无问题
  - `MOSS_SKIP_E2E=1 pnpm -r test` 全部通过
  - 主网 e2e 测试因离线跳过，需联网时验证零 warning

## 变更范围

| 路径 | 说明 |
|---|---|
| `packages/protocols/neverland/` | 新增协议适配器包，含 ABI、adapter、manifest、test、README |
| `packages/mcp-server/package.json` | 增加 `@themoss/protocol-neverland` 依赖 |
| `packages/mcp-server/src/server.ts` | 在 served catalog 注册 neverlandManifest |
| `.changeset/cold-grapes-walk.md` | 新增 changeset |

## 合约地址（Monad mainnet, chainId 143）

- Pool proxy：`0x80F00661b13CC5F6ccd3885bE7b4C9c67545D585`
- PoolDataProvider：`0xfd0b6b6F736376F7B99ee989c749007c7757fDba`

两个地址均通过 `eth_getCode` 在 `rpc.monad.xyz` 上验证。

## Review / Merge 状态

- 当前状态：PR 已提交，等待 Review
- 尚未收到 Review 或完成 Merge
