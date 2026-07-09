# Monad 钱包与测试网配置实验

## 实验目标

配置钱包并连接到 Monad Testnet，完成 Faucet 领水与第一笔链上交易，为 Week 1 的 Proof of Work 建立证据链。

## 环境

- 钱包: MetaMask / Rabby / OKX Wallet / 其他（待用户确认）
- 网络: Monad Testnet
- 官方文档: https://docs.monad.xyz/developer-essentials/testnets
- Faucet: https://faucet.monad.xyz

## 网络配置

| 字段 | 值 |
|------|-----|
| Network Name | `Monad Testnet` |
| RPC URL | `https://testnet-rpc.monad.xyz` |
| Chain ID | `10143` / `0x279f` |
| Currency Symbol | `MON` |
| Explorer 1 | https://testnet.monadvision.com |
| Explorer 2 | https://testnet.monadscan.com |

## RPC 验证

2026-07-09 实测：

```json
{"jsonrpc":"2.0","id":1,"result":"0x279f"}
```

说明：`0x279f` 转换为十进制为 `10143`，与官方文档一致。

## 配置步骤

1. 打开钱包扩展。
2. 添加自定义网络：Monad Testnet。
3. 填入 RPC URL、Chain ID、Currency Symbol、Explorer。
4. 切换到 Monad Testnet。
5. 打开 Faucet： https://faucet.monad.xyz
6. 领取测试 MON。
7. 保存网络配置、Faucet 成功、余额截图。
8. 发起第一笔小额测试网交易，或用 Remix 部署 `Gmonad.sol`。
9. 将交易哈希和 Explorer 链接记录到 `submissions/week-01/first-tx.md`。

## 记录

- 钱包地址: 待用户填写公开地址
- 测试代币余额: 待领取后填写
- Faucet 领取时间: 待填写
- 第一次交易哈希: 待填写
- Explorer 链接: 待填写

## 安全边界

- 不记录私钥。
- 不记录助记词。
- 不上传 keystore 文件。
- AI 只处理公开地址、公开交易哈希、公开 Explorer 链接和截图路径。

## 参考

- Monad 官方文档：https://docs.monad.xyz/
- Testnet 信息：https://docs.monad.xyz/developer-essentials/testnets
- Remix 部署指南：https://docs.monad.xyz/guides/deploy-smart-contract/remix
