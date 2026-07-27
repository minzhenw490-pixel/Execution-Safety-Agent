# 🛡️ Sentinel for Safe Execution

> **Don't trade naked.**
>
> 给 DeFi 小白用的交易安全助手 —— 发交易之前，先帮你扫一遍有没有坑。
>
> **详细：** 一个运行在 Monad Testnet 上的 Execution Safety Layer——多池报价、双层风险评估，决定放行或拦截

---

## 一句话定位

一个运行在 **Monad Testnet** 上的 Execution Safety Layer：

当用户用 USDC 进行 Swap 时，系统向多个候选池子获取报价，形成 `routes[]`，再评估 Token Risk 与 Pool Risk，最终决定 **ALLOW / REJECT / FALLBACK**。

---

## 问题

| 问题 | 说明 |
|------|------|
| 选池难 | 同样的交易对，不同池子报价不同，新手不知道选哪个 |
| 报价陷阱 | 报价最高的池子不一定安全——可能是假深度/有毒池 |
| 事后才知道 | 现有安全工具只在出事之后报警，不能在交易前拦截 |
| 看不懂 | 钱包提示全是技术术语，普通用户看不懂 |

---

## 方案

```
用户输入 Swap
    ↓
向多个池子分别报价 → 返回 routes[]
    ↓
Token Risk 评估（代币本身有没有问题）
Pool Risk 评估（池子深度/滑点/报价是否异常）
    ↓
🟢 ALLOW   → 安全路径，放行
🔴 REJECT  → 有风险，拦截 + 大白话原因
🟡 FALLBACK → 自动切到安全路径
    ↓
交易执行 + 事件记录
```

### 核心论点

**最佳报价 ≠ 最佳路线**

报价最高的路径不一定是最安全的。Sentinel 不只比价格，还比风险。

---

## 演示场景

| # | 场景 | 预期决策 | 说明 |
|:-:|------|:--------:|------|
| 1 | USDC → GOOD @ SAFE Pool | ✅ ALLOW | 正常交易，系统不误伤 |
| 2 | USDC → GOOD @ SHALLOW Pool | ⚠️ 展示问题 | 报价真实但滑点高，提示用户 |
| 3 | USDC → GOOD @ TOXIC Pool | 🔴 REJECT → 🟡 FALLBACK | 表面报价高，但池子有毒，切安全路 |
| 4 | USDC → BAD @ SAFE Pool | 🔴 REJECT | 池子正常但代币本身有问题 |

---

## 风险模型

### Token Risk（代币层）
- 合约权限是否异常
- 是否有风险标签
- 资产可信度

### Pool Risk（池子层）
- 流动性深度
- 滑点是否可接受
- 报价是否异常偏离参考价
- 历史失败率

---

## 技术架构

```
前端 (React + Vite)
    ↓ 调 API
报价服务 (/quote → 返回 routes[])
安全引擎 (/evaluate → 返回 decision)
执行层 (/execute → 链上交易)
事件层 (/events → 时间线)
    ↓
链上 (Solidity · Monad Testnet)
```

---

## 团队

| 角色 | 成员 | 方向 |
|------|------|------|
| 🎨 设计 | 酷可可 | UI/UX 设计 |
| 💻 前端 | Joy | Demo 页面开发 |
| 🔗 Dev A | Milli | 合约部署 |
| ⚙️ Dev B | Ni | 风控配置 + Token/Pool 搭建 |
| 🔧 Dev C | MINGHONG | 报价后端 + API |
| 🔧 Dev D | Boring | 后端 API + QA |
| 🧠 Dev E | Zelll | 规则引擎 |
| 📢 运营 | 77 | 产品文档 + 演示 |

---

## 部署

- **链：** Monad Testnet
- **代币：** GOOD / BAD / BAIT（自部署 ERC20）
- **池子：** SAFE / SHALLOW / TOXIC

---

## 链接

- GitHub: [github.com/YMH0417/sentinel-for-safe-execution](https://github.com/YMH0417/sentinel-for-safe-execution)
- Demo Video: （待补充）
- Pitch Deck: （待补充）
