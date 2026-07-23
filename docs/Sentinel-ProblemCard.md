# 🛡️ Problem & Mini Demo Card

## Sentinel for Safe Execution · Week 3 黑客松

---

### 🎯 目标用户

> 普通 **DeFi 交易者**，在 Monad 链上做 Swap 的**小散户**

---

### ❌ 核心问题

> 用户在 Swap 时**无法判断交易路径是否安全**，容易进入异常流动性池，导致**报价偏离、滑点亏损**

---

### 🔄 当前解决方式

> 钱包只负责签名交易，**不会告诉用户这笔交易是否存在风险**

---

### ✅ 我们的方案

> 在用户执行交易前，**Safety Agent** 自动检查多条候选路径的风险，输出 **ALLOW** / **REJECT** / **FALLBACK** 决策，帮用户避开高风险路径

> **Don't trade naked. 🛡️**

---

### 📦 Mini Demo 核心功能

```
输入 Swap → 获取 3 条 Route → Agent 评估 → 执行结果 → NFT 展示
```

| Route | 决策 | 评分 | 说明 |
|-------|------|------|------|
| **Route A** · Safe Pool | 🟢 **ALLOW** | 15 | 1000 USDT → 999 USDC |
| **Route B** · Risky Pool | 🔴 **REJECT** | 85 | 1000 USDT → 800 USDC |
| **Route C** · Moderate | 🟡 **FALLBACK** | 75 | 1000 USDT → 960 USDC |

**Demo 对比：**
- 🛡️ 有 Agent → 到账 **1002 MON** ✅
- ❌ 无 Agent → 到账 **978 MON**（亏损 22 MON）
- 节省 **+2.4%** 🎉
