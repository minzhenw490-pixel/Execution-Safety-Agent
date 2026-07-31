# 🏁 Hackathon Start Card — Sentinel for Safe Execution

> **Week 4 Day 5 · Choose Your First Move** — 确定 Build Sprint 第一步

---

## 项目信息

| 项目 | 内容 |
|------|------|
| **项目名称** | Sentinel for Safe Execution |
| **一句话介绍** | 给 DeFi 小白用的交易安全助手 |
| **目标用户** | 普通 DeFi 用户，尤其是链上交易新手 |
| **想解决的问题** | 用户做 Swap 之前，不知道哪条路径是安全的，等亏了才知道踩坑了 |

---

## 核心体验（第一版 Demo 只做一个动作）

### 用户是谁？
**小明**——刚进 Web3 的新手，会连钱包，但看不懂滑点、报价偏离这些术语。

### 用户要完成什么动作？
输入一笔 Swap（100 USDC → GOOD），系统自动检查多条路径，给出决策（放行 / 拦截 / 换路）+ 大白话原因。

### 完成后得到什么价值？
「我不用自己判断哪条路安全——系统提前帮我扫了一遍，还告诉我为什么。」

### 核心体验一句话
> **输入交易 → 多池报价 → 双层检查 → 大白话决策 → 安全到账**

---

## 真实实现 vs Mock 区分

### 🔴 必须真实运行
| 模块 | 说明 |
|------|------|
| Monad 测试链合约 | 代币 + 3 类池子（SAFE/SHALLOW/TOXIC）真实部署 |
| 多池报价接口 | /quote 返回真实 routes[] |
| 规则引擎 | Token Risk + Pool Risk 双层评估，输出 ALLOW/REJECT/FALLBACK |
| 链上执行 | 用户确认后真实上链 |

### 🟡 可以先 Mock
| 模块 | 方式 |
|------|------|
| 行情数据 | 预置 routes.json 样本数据 |
| AI 解释文案 | Zelll 规则引擎输出的固定模板（暂不接 LLM） |
| NFT 勋章 | Mock 数据展示（LV1→LV4 等级墙） |
| 部分后端 | DevD mock API → 逐步替换为真实链上 |

### ⚪ 本次明确不做
- ❌ 多链支持（只做 Monad）
- ❌ LLM 实时决策（只做规则引擎）
- ❌ 钱包插件（独立 Web 页面）
- ❌ 复杂 Dashboard 图表

---

## 为什么适合 Monad？

Monad 以高性能、高频交易著称。**链上速度越快，用户做决策的频率越高，踩坑的概率也越大。** Sentinel 在这个高速环境中充当冷静的智能守护者——交易越快，越需要交易前的冷静判断。

---

## Moss 使用情况

本次**不使用 Moss**。项目核心在 Agent 规则引擎（链下评估）+ 前端交互 + Monad 链上执行，不涉及 Moss 的模拟执行能力。

---

## 下一周（Build Sprint）第一步

### 最先验证的风险
**端到端 Demo 能不能跑通。** 具体拆成：

1. **Monad 测试链合约部署**（Milli）——代币 + 池子先跑起来
2. **报价接口链上联调**（MINGHONG + Boring）——/quote 返回真实数据
3. **规则引擎交付**（Zelll）——evaluateRoute 输出正确决策
4. **前端演示模式**（Joy）——5 个场景按钮，点一下切换
5. **Demo 视频录制**（77）——演示模式录屏提交

### 本周已完成（支撑下一步）
- ✅ 产品文档全套（PRD / 展示大纲 / Demo 脚本 v5.1 / 演讲稿定稿）
- ✅ 风险阈值定稿（报价偏离 0.8% / 失败率 20% / 池风险 70）
- ✅ 三条 Demo 路线定稿（route-a ALLOW / route-b REJECT / route-c FALLBACK）
- ✅ 用户调研验证（新人老玩家都重视安全；AI 只有建议权无执行权）
- ✅ Logo + 开场动画视觉

---

## 团队分工

| 成员 | 角色 | Build Sprint 第一步 |
|------|------|-------------------|
| 77 | 运营 / PM | Demo 视频录制、进度协调、文案 |
| 酷可可 | 设计 | NFT 勋章视觉、演示模式美化 |
| Joy | 前端 | 演示模式 5 场景按钮 |
| Milli | Dev · 合约 | Monad 测试链部署 |
| Ni | Dev · 风险 | 阈值配置联调 |
| MINGHONG | Dev · 报价 | /quote 接口链上化 |
| Boring | Dev · 后端 | API 全链路 + QA |
| Zelll | Dev · 规则引擎 | evaluateRoute 交付 |

---

*📅 Week 4 Day 5 · Web3 Career Build · 2026*
