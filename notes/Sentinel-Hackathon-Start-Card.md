# 🏁 Hackathon Start Card — Sentinel for Safe Execution

---

## 项目信息

| 项目 | 内容 |
|------|------|
| **项目名称** | Sentinel for Safe Execution |
| **一句话介绍** | 给 DeFi 用户用的交易安全助手。一个运行在 Monad 链上的 Execution Safety Layer，多池报价、双层风控 |
| **目标用户** | 普通 DeFi 用户，尤其是链上交易新手 |
| **想解决的问题** | 用户做 Swap 之前，不知道哪条路径是安全的，等亏了才知道踩坑了 |

---

## Demo 计划

### 用户可以完成的一个核心动作

用户在 Demo 页面上输入一笔 Swap（100 USDT → USDC），系统自动检查多条路径，输出决策结果（ALLOW / REJECT / FALLBACK），并用大白话解释原因。用户可以对比「有保护」和「没保护」两种方式的到账差异。

### 为什么适合 Monad

Monad 以高性能、高频交易著称。链上速度越快，用户做决策的频率越高，踩坑的概率也越大。Sentinel 在这个高速环境中充当冷静的智能守护者，帮助用户在快速交易中保持安全判断。

### 是否使用 Moss

本次不使用 Moss。项目核心在 Agent 规则引擎和前端交互，不涉及 Moss 的链上模拟执行能力。

---

## 开发范围

### 本次一定要完成什么

- ✅ 前端交易面板 + Dashboard + 成就页面
- ✅ 后端 API 全链路（quote → evaluate → execute → events）
- ✅ Agent 规则引擎（3 条规则 + 3 种决策）
- ✅ Monad 测试链合约部署（代币 + 交易池）
- ✅ 开场动画（15 秒像素风）
- ✅ 完整 Demo 展示（有保护 vs 无保护对比）
- ✅ 大白话文案覆盖所有提示

### 哪些部分可以使用组件 / Mock

| 模块 | 方式 |
|------|------|
| 交易数据 | Mock routes.json（3 条 Route 样本） |
| 风险阈值 | 硬编码 config（后续替换为配置文件） |
| AI 解释层 | 固定模板文案（暂不接 LLM） |
| NFT 勋章 | Mock 数据展示 |

### 本次明确不做什么

- ❌ 多链支持（只做 Monad）
- ❌ LLM 实时决策（只做规则引擎）
- ❌ 真实行情接入（用 mock 数据）
- ❌ 钱包插件（独立 Web 页面）
- ❌ 复杂 Dashboard 图表（只做评分+时间线）

---

## 团队信息

### 团队成员与分工

| 成员 | 角色 | 贡献 |
|------|------|------|
| 77 | 运营 / PM | 产品文档、Demo 脚本、展示大纲、进度协调 |
| 酷可可 | 设计 | UI 设计、Logo 设计、开场动画视觉 |
| Joy | 前端 | Demo 页面开发、API 对接 |
| Milli | Dev · 合约 | Monad 测试链合约部署 |
| Ni | Dev · 风险 | 风险阈值配置 |
| MINGHONG | Dev · 报价 | 多池 route 生成 / 后端 API |
| Boring | Dev · 后端 | 后端 API 全链路 |
| Zelll | Dev · 规则引擎 | Agent 规则引擎 |

### 下一步最先完成什么

1. Monad 测试链部署代币和交易池（Milli）
2. 后端 API 链上联调（Boring）
3. 规则引擎交付（Zelll）
4. 前端接入 API（Joy）

### 当前最大风险是什么

**规则引擎的准确率。** 如果 evaluateRoute 误报率太高（把安全路径判断为风险，或者漏掉真正的风险），用户会失去信任。Zelll 目前还在学习中，这是当前最大的不确定性。

---

*📅 Week 4 · Web3 Career Build · 2026*
