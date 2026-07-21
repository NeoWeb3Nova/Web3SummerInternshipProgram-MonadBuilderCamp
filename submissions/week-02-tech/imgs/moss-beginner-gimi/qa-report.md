# Moss 新手指南 · Gimi 配图 QA

## 批次结论

- 生成日期：2026-07-14
- 模型：`gpt-image-2-high`
- 角色参考：`/home/neo/.hermes/skills/gimi-illustration/assets/ip/gimi/reference-character.png`
- 图片数量：5/5
- 尺寸：全部为 1672×941（16:9）
- 角色：全部使用新版 WEB3 黑 T 男生，无旧马帽女孩元素

## 逐图结果

| 图片 | 角色锚点 | 核心表意 | 文字 | 版式污染 | 结果 |
|---|---|---|---|---|---|
| 01 一条命令 | 完整，唯一角色 | 1.5 MON → SIMULATE → WMON；钱包隔离 | 正确 | 无 | PASS |
| 02 四步边界 | 完整，唯一角色 | DISCOVER → LOAD → ACTION → SIMULATE；钱包在边界外 | 正确 | 无 | PASS（初版出现重复角色，编辑后复检通过） |
| 03 对账 | 完整，唯一角色 | EXPECTS / EFFECTS 天平对账；差异进入 WARNING | 正确 | 无 | PASS |
| 04 意图对齐 | 完整，唯一角色 | NO WARNING 后仍对齐 INTENT；STOP 手势明确 | 正确 | 无 | PASS |
| 05 安全交接 | 完整，唯一角色 | AGENT → MOSS → REVIEW → SIGN；签名笔留在用户侧 | 正确 | 无 | PASS |

## 通用检查

- 白底、黑色抖动线稿、软蓝主强调、软橙少量点睛：通过。
- 无九宫格、气泡、粉色渐变背景、白色贴纸描边：通过。
- 无马帽、动物耳、条纹背心、吊坠、裙子、厚底靴：通过。
- 与摸鱼绿正文兼容：通过；HTML 外框使用摸鱼绿主题的细边框与绿色图注衔接。
