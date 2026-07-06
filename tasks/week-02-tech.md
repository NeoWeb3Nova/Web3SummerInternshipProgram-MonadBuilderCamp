# Week 2 Tech Track: 技术与产品实现

## 本周目标

掌握 EVM / Monad 开发基础，完成一个简单合约与前端交互原型，并为 Week 3/4 的团队项目打基础。

开营仪式提醒：AI 可以快速写代码，但产品是否真的解决问题、能否稳定运行，仍需要人来判断、测试和复盘。

## Day-by-Day 任务

### Day 8: Solidity 与 EVM 基础

- [ ] 学习 Solidity 基本语法（变量、函数、修饰符、事件）
- [ ] 理解 EVM 兼容的意义：为什么以太坊工具可以迁到 Monad
- [ ] 完成一个 Counter / HelloWorld 合约
- [ ] 在 `experiments/week-02-contract/` 保存代码

### Day 9: Foundry / Hardhat 与测试

- [ ] 学习 `forge build`、`forge test`、`forge script`
- [ ] 为练习合约写基础测试
- [ ] 记录一次失败测试和修复过程
- [ ] 输出 `submissions/week-02-tech/test-log.md`

### Day 10: Monad Testnet 部署

- [ ] 配置 Monad Testnet RPC 和私钥环境变量
- [ ] 部署练习合约到 Monad Testnet
- [ ] 记录合约地址、部署交易哈希、Explorer 链接
- [ ] 输出 `submissions/week-02-tech/deploy.md`

### Day 11: 前端环境与钱包连接

- [ ] 使用 Vite + React 创建前端项目
- [ ] 安装 wagmi + viem 或 ethers.js
- [ ] 配置 Monad Testnet chain
- [ ] 实现 Connect Wallet 按钮

### Day 12: 合约交互

- [ ] 读取合约状态
- [ ] 实现写入/交易功能
- [ ] 显示 loading、success、error 状态
- [ ] 记录至少一次成功交易哈希

### Day 13: 产品化检查

- [ ] 从用户视角测试完整流程
- [ ] 写清楚这个 demo 解决什么问题，或只是技术练习
- [ ] 如果只是技术练习，提出一个 Week 3 可产品化方向
- [ ] 输出 `submissions/week-02-tech/product-notes.md`

### Day 14: 复盘与提交

- [ ] 完善 README
- [ ] 整理代码并提交到 GitHub
- [ ] 填写技术复盘
- [ ] 准备 Week 3 组队时可展示的 Demo 或代码片段

## 本周交付物

| 交付物 | 路径 | 状态 |
|--------|-------|------|
| 合约代码 | `experiments/week-02-contract/` | 待填写 |
| 合约测试 | `experiments/week-02-contract/test/` | 待填写 |
| 测试记录 | `submissions/week-02-tech/test-log.md` | 待填写 |
| 部署记录 | `submissions/week-02-tech/deploy.md` | 待填写 |
| 前端原型 | `experiments/week-02-frontend/` | 待填写 |
| 产品化笔记 | `submissions/week-02-tech/product-notes.md` | 待填写 |
| 技术复盘 | `submissions/week-02-tech/retro.md` | 待填写 |

## 学习资源

- Solidity 官方文档: https://docs.soliditylang.org/
- Foundry 书: https://book.getfoundry.sh/
- wagmi: https://wagmi.sh/
- viem: https://viem.sh/
- Monad 技术笔记: `docs/monad-technical-notes.md`
