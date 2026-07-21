# Week 2｜Challenge｜认识一个开源项目：Moss

> 学员：Neo  
> 方向：Dev Builder（Tech）  
> 初稿日期：2026-07-14  
> **架构同步：2026-07-20**（Capability Tree + Exhaustive Receipt）

## 提交信息

- GitHub 用户主页：https://github.com/NeoWeb3Nova
- GitHub Stars 页面：https://github.com/NeoWeb3Nova?tab=stars
- Moss 仓库：https://github.com/nishuzumi/moss
- Star 状态：已通过 GitHub API 验证（HTTP 204），且 Moss 显示在个人 Stars 页首项

## 100～200 字分享

Moss 把 Monad 上复杂的协议交互封装成 `discover → load → action → simulate`：Agent 发现能力、加载参数契约、获得未签名 **Capability 树**，再经 `debug_traceCall` 模拟抽出有序 Changes，由 Receipt 穷尽解析为可核对文字；任意 Warning 即停，签名权留给钱包与用户。它适合作为 DeFi 助手、金库策略与 Agent 钱包之间的签名前验证层，而不是替用户自动发交易的机器人。

> 正文字数以本地统计为准；叙事已从旧 Plan/expects 对账更新为 Capability/Receipt。

## 延伸证据

| 类型 | 路径 |
|------|------|
| 架构勘误索引 | `submissions/week-02-tech/moss-architecture-errata.md` |
| 入门修订 v2 | `submissions/week-02-tech/moss-beginner-guide-v2.md` |
| 公众号修订 v2 | `submissions/week-02-tech/moss-wechat-article-v2.md` |
| 本地通俗讲解 | `experiments/moss/docs/architecture-explained.zh-CN.md` |
| 深度学习笔记 | `experiments/moss/MOSS-STUDY-NOTES.md` |
| Exploration Log | `submissions/week-02-tech/github-exploration-log-moss.md`（正文为当时记录，见文首勘误） |
