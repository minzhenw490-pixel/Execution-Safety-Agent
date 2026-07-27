# 📋 PRD — Sentinel for Safe Execution

> **版本：** Hackathon v1.0
> **Slogan：** Don't trade naked. 🛡️
> **编写：** 77

---

## 1. 产品概述

**一句话定位：** 给 DeFi 小白用的交易安全助手

**详细版：** 一个运行在 Monad Testnet 上的 Execution Safety Layer——用户 Swap 之前，系统向多个候选池子分别报价，评估 Token Risk 与 Pool Risk，输出 ALLOW / REJECT / FALLBACK，并用大白话告诉用户原因。

**核心论点：** 最佳报价 ≠ 最佳路线。报价最高的路径不一定是最安全的。

---

## 2. 用户痛点

| 痛点 | 说明 |
|------|------|
| 选池难 | 不同池子报价不同，新手不知道选哪个 |
| 报价陷阱 | 报价高的池子可能有假深度/有毒 |
| 看不懂 | 钱包提示全是术语，普通用户看不懂 |
| 事后才知道 | 现有工具只在事后报警，不能在交易前拦截 |

---

## 3. 核心流程

```
用户输入 Swap
    ↓
向多个池子分别报价 → 返回 routes[]（含参考价）
    ↓
Token Risk 评估（代币合约/权限/风险标签）
Pool Risk 评估（流动性/滑点/报价偏离）
    ↓
🟢 ALLOW → 放行
🔴 REJECT → 拦截 + 大白话原因
🟡 FALLBACK → 自动切安全路径
    ↓
交易执行 + 事件记录
```

---

## 4. 演示场景

| # | 场景 | 决策 | 说明 |
|:-:|------|:----:|------|
| 1 | USDC → GOOD @ SAFE Pool | ✅ ALLOW | 正常交易，不误伤 |
| 2 | USDC → GOOD @ SHALLOW Pool | ⚠️ 提示 | 滑点过高，展示问题 |
| 3 | USDC → GOOD @ TOXIC Pool | 🔴 → 🟡 | 报价高但池子有毒，降级|
| 4 | USDC → BAD @ SAFE Pool | 🔴 REJECT | 池子正常但代币有问题 |

**资产：** GOOD / BAD / BAIT（3 个自部署 Token）
**池子：** SAFE / SHALLOW / TOXIC（3 类 Pool）

---

## 5. 风险模型

### Token Risk
- 合约权限是否异常
- 是否有风险标签
- 历史交易行为

### Pool Risk
- 流动性深度
- 滑点（priceImpactBps）
- 报价偏离参考价
- 历史失败率

---

## 6. 技术架构

```
前端 (React + Vite) → 用户页面
报价服务 (/quote) → 返回 routes[]
安全引擎 (/evaluate) → Token Risk + Pool Risk
执行层 (/execute) → 链上交易
事件层 (/events) → 时间线
链上 (Solidity · Monad Testnet)
```

---

## 7. MVP 范围

### ✅ 必须实现
- 多池报价 routes[] + 参考价
- Token Risk + Pool Risk 双层评估
- ALLOW / REJECT / FALLBACK 三种决策
- Safe / Unsafe 对比模式
- 交易 X 光弹窗（模拟结果预览）
- 事件时间线
- Dashboard + NFT 勋章墙

### ❌ 暂不实现
- 多链支持（只做 Monad）
- 复杂 LLM 决策（只用规则引擎）
- 真实行情接入（用 mock 数据）
- 钱包插件（独立 Web 页面）
- 跨链安全评估

---

## 8. 团队

| 角色 | 成员 |
|------|------|
| 🎨 设计 | 酷可可 |
| 💻 前端 | Joy |
| 🔗 Dev A 合约 | Milli |
| ⚙️ Dev B 风控+池子 | Ni |
| 🔧 Dev C 报价后端 | MINGHONG |
| 🔧 Dev D 后端+QA | Boring |
| 🧠 Dev E 规则引擎 | Zelll |
| 📢 运营/PM | 77 |

---

*Hackathon v1.0 · 2026*
