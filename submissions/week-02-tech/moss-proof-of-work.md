# Week 2 | Challenge | 留下属于自己的 Proof of Work

> 学员：Neo
> GitHub：NeoWeb3Nova
> 日期：2026-07-17
> Builder 身份：Dev Builder（Tech）
> 贡献项目：[nishuzumi/moss](https://github.com/nishuzumi/moss)

## 提交证明类型

Open Source Contribution Log（基于真实 Pull Request）

## 1. GitHub PR 链接

https://github.com/NeoWeb3Nova/moss/pull/1

PR 标题：`feat(protocols): add Neverland lending adapter`

## 2. GitHub 用户主页

https://github.com/NeoWeb3Nova

## 3. 贡献内容

为 Moss 新增 `@themoss/protocol-neverland` 协议适配器，让 AI Agent 可以通过统一接口安全调用 Monad 主网上的 Neverland（Aave V3 借贷市场）：

- `supply`：存入 ERC-20 资产获取 aToken 收益
- `withdraw`：提取资产
- `accountData`：查询账户健康度、抵押品、债务等

关键设计：

- aToken 地址运行时从 `PoolDataProvider` 解析，避免硬编码过时
- 非 native 资产 supply 时嵌套 ERC-20 `approve` **子 Capability**（Capability 树，非旧 Plan）
- `@Receipt` 解析 `Supply` / `Withdraw` 等 Changes，满足穷尽覆盖
- 所有合约地址均通过 `eth_getCode` 在 Monad mainnet 上验证

> 架构说明：Neverland adapter 落在 Capability/Receipt 框架上。若旧笔记写「quantified expects」，以现行代码与 [`moss-architecture-errata.md`](./moss-architecture-errata.md) 为准。

## 4. 合约地址（Monad mainnet, chainId 143）

- Pool proxy：`0x80F00661b13CC5F6ccd3885bE7b4C9c67545D585`
- PoolDataProvider：`0xfd0b6b6F736376F7B99ee989c749007c7757fDba`

## 5. 本地验证证据

全部命令真实执行并通过：

```bash
pnpm -r build          # 通过
pnpm -r typecheck      # 通过
pnpm biome check .     # 无问题
MOSS_SKIP_E2E=1 pnpm -r test  # 全部通过
```

- 离线 shape 测试：3 passed
- 主网 e2e 测试：2 skipped（离线），需联网验证零 warning

## 6. 父仓库提交

- 本地路径：`/home/neo/workspace/projects/Web3SummerInternshipProgram-MonadBuilderCamp`
- 提交文件：`submissions/week-02-tech/moss-proof-of-work.md`
- 父仓库 Commit：[`97f01a2`](https://github.com/NeoWeb3Nova/Web3SummerInternshipProgram-MonadBuilderCamp/commit/97f01a2)

## 7. 历史相关贡献

本次 Proof of Work 之外，本周还向 Moss 上游提交了另一个 PR：

- PR：https://github.com/nishuzumi/moss/pull/36
- 类型：Core Bug Fix
- 标题：`fix(core): reject unsafe numeric uint inputs`
- 证据：`submissions/week-02-tech/moss-open-source-contribution-evidence.md`
- 状态：等待 Maintainer 批准 Actions

## 8. 当前 Review / Merge 状态

- PR #1（Neverland adapter）：已提交，等待 Review
- PR #36（unsafe uint fix）：已提交，等待 Maintainer 批准 GitHub Actions
- 均无 Maintainer Review 或 Merge

## 9. 复盘

### 目标
完成一次真实、可验证的开源贡献，为 GitHub 留下 Proof of Work。

### 动作
1. 阅读 Moss ADR 与 template，确认 Adapter 设计边界
2. 选择 Monad-native 的 Neverland 借贷协议
3. 实现 supply / withdraw / accountData 三个能力
4. 补全 ABI 来源、README、changeset、测试
5. 运行 build / typecheck / lint / test 全部门
6. 推送分支并创建 PR
7. 在父仓库提交 Open Source Contribution Log

### 结果
- 形成 1 个可 Review 的 PR
- 产出完整技术证据与提交文件
- 父仓库 master 已更新

### 问题
- 离线环境下主网 e2e 无法运行，需联网补零 warning 验证
- 之前 unsafe uint PR 上游 Core 正在重构，合并概率不确定，但贡献过程完整

### 下一步
- 等待 Maintainer Review
- 联网运行完整 e2e，确认主网 simulate 零 warning
- Review / Merge 发生后补充对应链接
