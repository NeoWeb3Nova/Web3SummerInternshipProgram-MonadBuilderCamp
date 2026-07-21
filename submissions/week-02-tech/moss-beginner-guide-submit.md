# Moss 新手入门指南｜课程提交

## 文章标题

《第一次跑通 Moss：零私钥完成一笔 Monad 链上交易模拟》

## 文章链接

- **现行修订版（推荐）**：[`moss-beginner-guide-v2.md`](./moss-beginner-guide-v2.md)  
  https://github.com/NeoWeb3Nova/Web3SummerInternshipProgram-MonadBuilderCamp/blob/master/submissions/week-02-tech/moss-beginner-guide-v2.md
- Week 2 历史稿（Plan/expects）：[`moss-beginner-guide.md`](./moss-beginner-guide.md)
- 勘误索引：[`moss-architecture-errata.md`](./moss-architecture-errata.md)

## 主题说明

本教程面向 Moss 新手，以零私钥 WMON 包装实验跑通四步流程；**v2** 按 Capability 树与 Receipt 穷尽覆盖重写，并给出 MCP 接入与贡献路径。

## 公众号发布产物

- Markdown（现行）：`moss-beginner-guide-v2.md`
- Markdown（历史 Week 2）：`moss-beginner-guide.md`
- 公众号干净正文：`moss-beginner-guide_排版_摸鱼绿(moyu-green).html`
- 一键复制预览：`moss-beginner-guide_排版_摸鱼绿(moyu-green)_预览.html`
- 封面高清原图：`moss-beginner-guide-cover-original.png`
- 微信公众号封面：`moss-beginner-guide-cover-900x383.png`

## 实践证据

- Moss 源码提交：`94adfea`
- Node.js：`v22.22.2`
- pnpm：`11.10.0`
- `pnpm build`：通过
- `MOSS_SKIP_E2E=1 pnpm test`：通过
- `pnpm --filter @themoss/example-simple-flow wrap`：通过，`warnings: []`
