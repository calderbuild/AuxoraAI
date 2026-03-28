---
title: Auxora.ai 定价页 A/B 测试方案
type: report
date: 2026-03-27
author: Calder
audience: Hui Li (CEO)
---

# Auxora.ai 定价页 A/B 测试方案

## 前提

Auxora 4/1 正式发布，当前 7 个付费用户，流量极低。本方案基于 CRO 审计的结构性问题设计，目标是 launch 后用最小流量验证最高杠杆的假设。

样本量公式统一采用：`n = 16 * p(1-p) / (p1-p0)^2`，alpha = 0.05，power = 0.80。

---

## 测试前必须修复的前置条件

| # | 问题 | 原因 |
|---|------|------|
| 1 | `/report` 路由失效（回退首页） | 5 个 CTA 指向该路由，转化链断裂，测试数据无意义 |
| 2 | 价格数字统一（$49 / $200 / $4.99 互相矛盾） | 无法区分"价格本身"和"价格混乱"的影响 |
| 3 | GA4 代码接入 | 当前网站无追踪代码，无法采集测试数据 |
| 4 | `demo-poster.jpg` 404 修复 | 视频缩略图空白影响全局信任感知 |
| 5 | Copyright 更新为 2026 | 细节信任问题，影响基线转化率 |

---

## 测试 1：CTA 路径统一（最高优先级）

**假设**：3 条并行 CTA 路径合并为 1 条主路径，能提高首页 CTA 点击率。

| 维度 | 控制组（当前） | 实验组 |
|------|--------------|--------|
| 导航栏 | "Get More Revenue" + "Get started" 双按钮 | "Sign in"（文字链）+ "Get Free Snapshot"（主按钮） |
| Hero CTA | "Get New Customers in 48 Hours" -> 页底邮件表单 | "See Your Free Market Snapshot" -> /report |
| 定价卡 | Free/Strategy -> /report（失效），Launch -> 页底表单 | 各卡指向对应功能页（/report?plan=free 等） |

- **Primary Metric**：首页 CTA 总点击率
- **Secondary**：/report 到达率、注册完成率、bounce rate
- **样本量**：控制组 CTR 3% -> 期望 5%，需约 3,100 访客（1,536/组）
- **运行时间**：日均 50-100 UV，约 5-9 周
- **理由**：CTA 混乱是最大的转化杀手（Hick's Law），修复后所有后续测试基线都会改善

---

## 测试 2：Hero Headline 方向

**假设**：结果导向 headline 比品牌导向 headline 产生更高的 CTA 点击率。

| 维度 | 控制组 | 实验组 |
|------|--------|--------|
| H1 | "Your AI growth team. Done for you." | "Get new customers in 48 hours. No agency. No DIY." |
| Sub-headline | 不变 | 不变 |

- **Primary Metric**：Hero CTA 点击率
- **Secondary**：页面停留时间、scroll depth 到定价区的比例
- **样本量**：控制组 CTR 5% -> 期望 8%，需约 2,200 访客（1,083/组）
- **运行时间**：日均 50-100 UV，约 3-6 周
- **理由**：100% 访客看到，测试成本低（只改一行文案）。须在测试 1 之后运行

---

## 测试 3：定价卡锚点策略

**假设**："Most Popular" 标签从 $49 移到 $4.99，以 $49 作价格锚点，能提高 $4.99 付费转化率。

| 维度 | 控制组 | 实验组 |
|------|--------|--------|
| 视觉高亮 | $49 Launch 标 "Most Popular" | $4.99 Strategy 标 "Most Popular" |
| $49 卡片 | 高亮蓝色边框 | 普通样式 + "Full Service" 标签 |

- **Primary Metric**：$4.99 Strategy 购买转化率
- **Secondary**：$49 转化率（确认无显著下降）
- **样本量**：控制组转化率 1% -> 期望 2.5%，需约 2,500 访客（1,223/组）
- **运行时间**：日均 50-100 UV，约 4-7 周
- **理由**：$4.99 是最低摩擦付费入口，验证 PMF 的关键价格点。依赖支付流程上线

---

## 测试 4：社会证明真实性

**假设**：移除不可验证的 "4.9/5, 53 early users"，替换为真实客户成果数据，不会降低转化率。

| 维度 | 控制组 | 实验组 |
|------|--------|--------|
| 信任标记 | "4.9/5 . 53 early users"（无来源） | "7 businesses launched in beta" + 真实客户 one-liner |
| Testimonial | 4 条（名字首字母，无照片） | 2-3 条 + 真实头像 + LinkedIn 链接 |

- **Primary Metric**：注册完成率
- **Secondary**：定价区 CTA 点击率、bounce rate
- **样本量**：控制组注册率 2%，检测最小变化 1%（非劣效性），需约 7,800 访客
- **运行时间**：日均 50-100 UV，约 11-22 周。建议作为长期测试
- **理由**：问题严重（Sarah K. 人设不一致），但样本量最大且需客户授权，优先级最低

---

## 优先级总结

| 顺序 | 测试 | 前置条件 | 最小样本 | 周期 |
|------|------|---------|---------|----|
| 1 | CTA 路径统一 | /report 修复 + GA4 接入 | 3,100 | 5-9 周 |
| 2 | Hero Headline | 测试 1 完成 | 2,200 | 3-6 周 |
| 3 | 定价卡锚点 | 支付流程上线 | 2,500 | 4-7 周 |
| 4 | 社会证明 | 真实客户授权 | 7,800 | 11-22 周 |

测试 1、2 串行运行。测试 3、4 改动区域不重叠，流量允许时可并行。

---

## 工具推荐

| 工具 | 理由 |
|------|------|
| **PostHog**（首选） | 免费版支持 feature flags + A/B testing + analytics，1M events/月，自带显著性计算 |
| VWO Starter（备选） | 可视化编辑器改页面，不需工程师，免费版 10K 访客/月 |
| Hotjar（辅助） | 免费版 35 sessions/天的录屏和 heatmap，辅助解读定量结果 |

**不推荐**：Optimizely（企业定价）、Google Optimize（2023 年已停止服务）。

**务实建议**：日均 <100 UV 阶段，测试 1 可以跳过 A/B 工具，直接实施改进方案后用 GA4 before/after 对比。快速迭代比统计严谨性更重要。
