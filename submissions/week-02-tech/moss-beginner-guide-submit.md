# Moss 新手入门指南｜课程提交

## 文章标题

《第一次跑通 Moss：零私钥完成一笔 Monad 链上交易模拟》

## 文章链接

https://github.com/NeoWeb3Nova/Web3SummerInternshipProgram-MonadBuilderCamp/blob/master/submissions/week-02-tech/moss-beginner-guide.md

## 主题说明

本教程面向 Moss 新手，以零私钥、零资金的 WMON 包装实验跑通四步流程，逐步解释 Plan、预期、实际效果和警告，并给出环境排错、MCP 接入与开源贡献路径。

计数：54 个汉字，77 个非空白字符，符合 50～100 字要求。

## 公众号发布产物

- Markdown：`moss-beginner-guide.md`
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
