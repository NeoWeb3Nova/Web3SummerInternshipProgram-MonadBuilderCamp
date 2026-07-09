# Monad Testnet 网络配置

> 来源优先级：Monad 官方文档与实时 RPC 验证。私钥 / 助记词不得写入本仓库。

## 来源

- 官方文档： https://docs.monad.xyz/developer-essentials/testnets
- Faucet： https://faucet.monad.xyz
- 记录日期：2026-07-09
- 实测 RPC：`https://testnet-rpc.monad.xyz`
- 实测方法：JSON-RPC `eth_chainId`
- 实测结果：`0x279f` = `10143`

---

## 网络参数

| 字段 | 值 | 来源/备注 |
|------|-----|----------|
| 网络名称 | `Monad Testnet` | Monad 官方文档 |
| RPC URL | `https://testnet-rpc.monad.xyz` | 官方 Public RPC，QuickNode，50 rps |
| Chain ID | `10143` / `0x279f` | 官方文档 + JSON-RPC 实测 |
| 货币符号 | `MON` | Monad 官方文档 |
| 区块浏览器 MonadVision | https://testnet.monadvision.com | 官方文档 |
| 区块浏览器 Monadscan | https://testnet.monadscan.com | 官方文档 |
| Network visualization | https://www.gmonads.com/?network=testnet | 官方文档 |
| App hub | https://testnet.monad.xyz/ | 官方文档 |
| Faucet | https://faucet.monad.xyz | 官方文档 |
| 当前版本 / revision | `v0.14.5` / `MONAD_NINE` | 官方文档记录时点 |

## 备用 / 其他公共 RPC

| RPC URL | Provider | 限制 / 备注 |
|------|----------|-------------|
| `https://testnet-rpc.monad.xyz` | QuickNode | 50 rps；Batch 100；Archive ✅；`eth_call` / `eth_estimateGas` 25 rps |
| `https://rpc.ankr.com/monad_testnet` | Ankr | 300 reqs / 10s；12000 reqs / 10 min；Archive ❌；`debug_*` 不可用 |
| `https://rpc-testnet.monadinfra.com` | Monad Foundation | 20 rps；Batch 不允许；Archive ✅ |

## Faucet 信息

| 项目 | 值 |
|------|-----|
| 官方 Faucet | https://faucet.monad.xyz |
| 领取条件 | 待用户实际操作后补充（可能需要钱包连接 / CAPTCHA / 社交验证） |
| 领取数量 | 待记录 |
| 领取时间 | 待记录 |

## 钱包配置记录

| 项目 | 值 |
|------|-----|
| 钱包类型 | MetaMask / Rabby / OKX Wallet / 其他（待确认） |
| 钱包地址 | `0x...`（只记录公开地址，待用户填写） |
| 是否切换到 Monad Testnet | 待勾选 |
| 测试币余额 | 待记录 |

## 截图/证据

- 钱包网络配置截图：`assets/week-01/monad-testnet-network-config.png`（待保存）
- Faucet 领取成功截图：`assets/week-01/monad-testnet-faucet.png`（待保存）
- 钱包余额截图：`assets/week-01/monad-testnet-balance.png`（待保存）

## Build Log

- 2026-07-08：创建网络配置提交物模板，等待实际钱包配置和领水后回填参数。
- 2026-07-09：从 Monad 官方文档确认 Testnet 参数；用 JSON-RPC 实测 `https://testnet-rpc.monad.xyz` 返回 `eth_chainId = 0x279f`。
