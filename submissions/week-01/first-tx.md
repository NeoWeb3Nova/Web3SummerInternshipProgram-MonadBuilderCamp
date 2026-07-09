# 第一笔 Monad Testnet 链上交易记录

## 目标

完成第一笔 Monad Testnet 转账或合约交互，并留下可验证的 Proof of Work。

## 前置条件

- [x] 已确认 Monad Testnet 网络参数
- [x] 已验证 RPC `eth_chainId = 0x279f` / `10143`
- [ ] 已在钱包中添加 Monad Testnet
- [ ] 已从 Faucet 领取测试 MON
- [ ] 已保存钱包余额截图

## 可选路径 A：小额转账

适合目标：最快完成第一笔链上交易。

步骤：

1. 钱包切换到 Monad Testnet。
2. 确认余额中有测试 MON。
3. 向自己的另一个测试地址或可信测试地址发送一笔极小额 MON。
4. 等待交易确认。
5. 复制交易哈希和 Explorer 链接。

## 可选路径 B：Remix 部署 Gmonad 合约

适合目标：比转账更像 Builder Proof of Work。

官方指南： https://docs.monad.xyz/guides/deploy-smart-contract/remix

合约模板：

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.24;

contract Gmonad {
    string public greeting;

    constructor(string memory _greeting) {
        greeting = _greeting;
    }

    function setGreeting(string calldata _greeting) external {
        greeting = _greeting;
    }
}
```

建议 constructor 参数：

```text
gmonad from Neo Day 4
```

部署后可继续调用 `setGreeting`，形成第二笔交互记录。

## 实际交易记录

| 字段 | 值 |
|------|-----|
| 日期 | 2026-07-09 |
| 交易类型 | 小额转账 / Remix 合约部署 / 合约交互（待选择） |
| 钱包地址 | `0x...`（只填公开地址） |
| 目标地址 / 合约地址 | 待填写 |
| 交易哈希 | 待填写 |
| Explorer 链接 | 待填写 |
| Gas / Fee | 待填写 |
| 状态 | 待确认 |

## 截图证据

- 钱包交易确认截图：`assets/week-01/first-tx-wallet-confirm.png`（待保存）
- Explorer 交易详情截图：`assets/week-01/first-tx-explorer.png`（待保存）
- 若部署合约：Remix deployed contracts 截图：`assets/week-01/remix-gmonad-deployed.png`（待保存）

## 我做了什么

待交易完成后填写：

- 我选择了哪条路径：
- 为什么选择这条路径：
- 实际操作步骤：

## 为什么成功

待交易完成后填写：

- 网络配置是否正确：
- 钱包余额是否足够：
- 交易是否被 Explorer 收录：

## 遇到的问题

待交易完成后填写：

- Faucet 是否成功：
- 钱包是否弹窗：
- RPC 是否卡顿：
- Explorer 是否延迟：

## 今日反思

链上 Proof of Work 的核心不是截图，而是可复查的公开记录。交易哈希和 Explorer 链接让学习过程从“我学过”变成“我做过”。
