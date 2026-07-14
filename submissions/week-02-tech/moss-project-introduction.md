# Week 2｜Challenge｜认识一个开源项目：Moss

> 学员：Neo
> 方向：Dev Builder（Tech）
> 日期：2026-07-14

## 提交信息

- GitHub 用户主页：https://github.com/NeoWeb3Nova
- GitHub Stars 页面：https://github.com/NeoWeb3Nova?tab=stars
- Moss 仓库：https://github.com/nishuzumi/moss
- Star 状态：已通过 GitHub API 验证（HTTP 204），且 Moss 显示在个人 Stars 页首项

## 100～200 字分享

Moss 把 Monad 上复杂的协议交互封装成 `discover → load → action → simulate` 的统一能力，让 AI Agent 不必自行拼装 ABI、地址和 calldata。它先生成未签名交易，再基于真实链上状态模拟并核对资金流，出现异常就停止，把最终签名权留给用户。我认为它未来可用于 DeFi 交易助手、自动化金库、DAO 财库和跨协议策略执行，成为 Agent 与钱包之间的安全执行层。

> 正文共 192 个非空白字符，符合 100～200 字要求。

## 延伸证据

- Moss 深度学习笔记：`experiments/moss/MOSS-STUDY-NOTES.md`
- Moss Exploration Log：`submissions/week-02-tech/github-exploration-log-moss.md`
- MockVault 适配器草稿：`experiments/moss/packages/protocols/mockvault/`
