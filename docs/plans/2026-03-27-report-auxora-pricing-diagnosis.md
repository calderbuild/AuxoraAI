---
title: Auxora.ai 定价策略诊断
type: report
date: 2026-03-27
author: Calder
audience: Hui Li (CEO)
---

# Auxora.ai 定价策略诊断

## 结论

Auxora 首页同时出现 $4.99、$49、$200 三个价格，互相矛盾。根本原因不是笔误，而是**定价叙事没有统一** -- 三个递进的产品层级（免费快照 / $4.99 报告 / $49 全栈执行）没有被清晰地串成一条线，同时 $200 这个旧价格残留在页面上制造混乱。

---

## 1. 当前页面上的价格出现位置

| 位置 | 文案 | 价格 |
|------|------|------|
| Hero 区 | "Starting at $49" | $49 |
| Hero 下方标签 | "Starts at $49" | $49 |
| 定价卡 Free 层 | "$0, no credit card" | $0 |
| 定价卡 Strategy 层 | "$4.99 one-time" | $4.99 |
| 定价卡 Launch 层 | "$49 token-based" | $49 |
| How It Works Step 1 | "Tell us your goal -- from $49" | $49 |
| How It Works Step 2 | "We build your full marketing stack -- $200" | $200 |
| FAQ | "What exactly does Auxora build for $200?" | $200 |
| Footer | "From $49" | $49 |
| 定价区说明文 | "from $49 -- and we only earn a revenue share..." | $49 |
| Revenue share 说明 | "ROAS reaches >= 0.7x" | 未标比例 |

**用户的心理活动**：

1. 看到 Hero "Starting at $49" -> 锚定 $49
2. 滚到定价卡，看到 $4.99 -> "等等，不是 $49 起吗？"
3. 滚到 How It Works Step 2 "$200" -> "什么？$200？$49 和 $200 什么关系？"
4. 看到 FAQ "$200" -> "到底要付多少钱？"
5. 放弃，离开

---

## 2. Auxora 实际有几个产品？

交叉对照定价卡、里程碑清单和产品内页，Auxora 实际是 **3 个递进的产品层级**：

| 层级 | 交付物 | 价格 | 用户动作 |
|------|--------|------|---------|
| **Snapshot**（免费） | 竞品概览 + 搜索量 + 获客成本估算 + 渠道推荐 | $0 | 输入业务信息，2 分钟出结果 |
| **Strategy Report** | 完整 GTM 报告：ICP 分析 + 定位 + SEO 关键词 + 竞品地图 + 轻量 Q&A | $4.99 一次性 | 3 问访谈后生成，付费解锁完整版 |
| **Launch** | 全栈执行：Landing Page + 广告素材 + Campaign 设置 + SEO 文案 + 邮件 flow | $49 起（token-based）| 48 小时交付，后续 revenue share |

这三个层级的逻辑是 **"看一眼 -> 深入了解 -> 帮你全做"**，本身是很好的漏斗设计。问题在于页面没有把这条线讲清楚。

---

## 3. $200 到底是什么？

$200 出现在两个地方：
- How It Works Step 2："We build your full marketing stack -- $200"
- FAQ："What exactly does Auxora build for $200?"

两种可能：

| 可能性 | 如果是这样 | 应该怎么做 |
|--------|-----------|-----------|
| $200 是旧版定价，已被 $49 token-based 替代 | 页面残留了旧文案 | 立即删除所有 $200，统一为 $49 |
| $200 是完整服务的真实价格，$49 只是首次充值/入门价 | 定价卡标的 $49 具有误导性 | 定价卡改为 "From $49" 并注明 "Full stack build: $200" |

**建议**：需要 Hui 确认 $200 的定义，然后统一。

---

## 4. "token-based" 没有解释

定价卡 Launch 层写了 "$49 token-based"，但整个页面没有解释：
- 什么是 token？
- $49 包含多少 token？
- 用完了怎么办？
- 怎么买更多？

对 solopreneur 用户来说，"token" 是一个技术概念，会增加决策摩擦。

**建议二选一**：
- **方案 A**（推荐）：不提 token，改为 "$49 one-time setup"。后续 token 消耗在产品内解释
- **方案 B**：保留 token 概念，但加一行说明 "$49 includes enough credits for 1 full campaign build"

---

## 5. Revenue share 不透明

页面说 "Revenue share only kicks in after your ROAS reaches >= 0.7x"，"We earn after you do"。

理念很好，但缺失关键信息：
- Revenue share 的比例是多少？10%？20%？
- 是按广告收入还是总收入计算？
- 有没有上限？

**影响**：用户不知道后续要付多少，会犹豫下单。即使不想公开精确比例，也应该给一个范围（"typically 10-15% of ad-attributed revenue"）。

---

## 6. 竞品价格定位

| 替代方案 | 价格 | 做什么 | 用户自己做多少 |
|---------|------|--------|--------------|
| Marketing agency | $2,000+ 设置 + $1,000-5,000/月 | 全栈执行 | 几乎不用自己做 |
| GoHighLevel | $97-497/月 | DIY 平台 | 用户自己做所有事 |
| Jasper AI | $49-125/月 | 只做文案 | 用户自己做策略和投放 |
| Mailchimp | $13-350/月 | 只做邮件 | 用户自己做其他渠道 |
| **Auxora** | **$4.99 报告 + $49 全栈** | **AI done-for-you** | **几乎不用自己做** |

Auxora 的定价优势明显：**agency 级别的交付，工具级别的价格**。$49 vs $2,000+ 的对比框架（首页的 Agency vs Auxora 对比表）非常有力。

风险：价格太低可能让用户怀疑质量 -- "$49 就能做 $2,000 的事？靠谱吗？" 这就是为什么信任元素（客户证言、真实案例、数据）特别重要。

---

## 7. $4.99 -> $49 的跳跃分析

| 升级路径 | 价格差 | 百分比跳跃 | 价值感知跳跃 |
|---------|--------|-----------|------------|
| Free -> $4.99 | +$4.99 | 从 0 到付费 | 合理（付费看更多内容） |
| $4.99 -> $49 | +$44.01 | +880% | 巨大（从"看报告"到"帮你做所有事"） |

这个跳跃本身不是问题 -- $4.99 是一个经典的 **"land and expand" 钩子**：

1. 用户花 $4.99 买报告，风险极低
2. 报告质量好，用户产生信任
3. 报告末尾展示 "如果你想让我们执行这个策略，$49 即可启动"
4. 用户已经看到了策略，知道要做什么，只是缺执行力 -> 自然升级

**要让这个策略生效的前提**：
- $4.99 报告必须足够好（当前 dogfooding 显示质量中上，但有数据准确性问题）
- 报告末尾必须有清晰的 upsell CTA（"Ready to execute? Launch for $49"）
- $49 的交付物要具体列出（"1 landing page + 2 ad creatives + 1 live campaign + email flow"），不能只说 "we build everything"

---

## 8. 建议的统一定价叙事

### 首页定价表述统一方案

**Hero 区**：
- 当前："Starting at $49" -> 和 $4.99 矛盾
- 建议改为："Try free. Strategy for $4.99. Full launch $49." 或 "See your market opportunity -- free"

**How It Works**：
- Step 1："Tell us about your business"（不标价格）
- Step 2："Get your GTM strategy -- $4.99"
- Step 3："We build and launch everything -- $49"
- Step 4："Scale on results -- revenue share after ROAS >= 0.7x"

**定价卡**：保持 Free / $4.99 / $49 三层，删除所有 $200

**FAQ**：
- "What exactly does Auxora build for $200?" -> 改为 "What exactly does Auxora build for $49?"

**Footer**：
- "From $49" -> "From $4.99" 或 "Free to start"

### 定价卡 CTA 统一方案

| 层级 | CTA 文案 | 指向 |
|------|---------|------|
| Free ($0) | "See my market snapshot" | /report（无需登录） |
| Strategy ($4.99) | "Get my strategy report" | /report -> 付费解锁 |
| Launch ($49) | "Launch my marketing" | /signup?plan=launch |

所有 CTA 指向实际可用的页面，不再跳到页底邮件表单。

---

## 9. 需要 Hui 确认的决策

| # | 问题 | 选项 | 影响 |
|---|------|------|------|
| 1 | $200 是否还存在？ | A: 已被 $49 替代（删除所有 $200）/ B: $200 是完整价格（$49 是入门价） | 定价卡和全页文案需要对应修改 |
| 2 | "token-based" 要不要在首页解释？ | A: 不提 token，改为 "$49 one-time"（推荐）/ B: 解释 token 含量 | 影响用户对价格的理解 |
| 3 | Revenue share 比例是多少？ | 需要给一个数字或范围 | 影响用户是否敢下单 |
| 4 | Hero "Starting at" 应该写什么？ | A: "Free to start" / B: "From $4.99" / C: 保持 "$49" | 影响用户对价格的第一印象 |
| 5 | $4.99 报告末尾有没有 upsell 到 $49 的 CTA？ | 如果没有，需要加 | $4.99 -> $49 转化的关键路径 |

这些是商业决策，不是工程问题。确认后页面修改是简单的。
