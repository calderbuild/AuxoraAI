---
title: Auxora Dogfooding 调研报告 & GTM 执行规划
type: report
date: 2026-03-25
author: Calder
audience: Hui Li (CEO)
---

# Auxora Dogfooding 调研报告 & GTM 执行规划

## 一、报告目的

Calder 入职第一周的产品深度体验和调研成果。目的：

1. 用 Auxora 分析真实客户网站，评估产品输出质量
2. 完成 app.auxora.ai 的 SEO 审计，识别技术问题
3. 基于发现，制定 90 天 GTM 执行计划

---

## 二、产品测试：4 个 Case 的对比

### 测试方法

用 Auxora 分析 4 个不同的业务场景，对比输出质量。

### 结果汇总

| Case | 输入方式 | 竞品选择 | 建议质量 | 数据准确度 |
|------|---------|---------|---------|----------|
| **Auxora 自身** (URL: app.auxora.ai) | URL | Monday.com / ClickUp / Notion -- **选错了**（这些是生产力工具不是营销工具） | 一般 | **7/10 数据有偏差或疑似虚构** |
| **Therapist** (URL: herecounseling.com) | URL | BetterHelp / Talkspace / Psychology Today -- **选对了** | 优秀 | 待验证，数字合理性明显好于 Case 1 |
| **Pest Control** (文字描述) | 文字 | 未出报告，聊天建议 | **非常好** -- 先诊断产能瓶颈再推渠道 | 具体数字（$15-30/lead, 30-50% 转化率）合理 |
| **Freelance Consultant** (文字描述) | 文字 | 未出报告，聊天建议 | **非常好** -- 推 LinkedIn 内容而非广告 | LinkedIn CPC $8-12 合理 |

### 关键发现

**1. 竞品选择高度依赖 business profile 提取质量**

- 用 app.auxora.ai 的 URL 时，产品提取出"AI Growth Operating System"这个泛描述 → 选了 Monday.com/ClickUp/Notion（错误）
- 用 herecounseling.com 的 URL 时，提取出"therapy/counseling practice" → 选了 BetterHelp/Talkspace/Psychology Today（正确）
- **结论**：竞品选择逻辑本身没问题，问题出在 business profile 提取。当网站内容足够垂直（如 therapy 网站），提取准确；当网站描述较泛（如 AI SaaS），提取泛化导致竞品偏移

**2. 聊天模式的建议质量 >> GTM Report 的数据质量**

- 聊天模式每次都给出了行业特定的精准建议（therapist → SEO + local Google Ads; pest control → 先解决产能再做 Google LSA; consultant → LinkedIn 内容）
- GTM Report 的数据部分（市场规模、流量数字、CAC 估算）存在虚构风险

**3. Auxora 自分析自己是最差的 case**

- 因为 Auxora 的 landing page 同时面向多个行业（therapist + pest control + consultant + ...），产品无法确定这是哪个行业，导致 profile 泛化
- 真实客户的网站（只做一个行业）不会有这个问题

### GTM Report 数据验证（Case 1: Auxora 自身）

对 Auxora 自身 GTM Report 的 10 个数据声称做了逐条验证：

| 声称 | 实际 | 判定 |
|------|------|------|
| AI 市场 $87.3B | 真实 $174-244B (2025) | 偏低 2-3x |
| Monday.com 18.4M 月访客 | 真实 ~41M | 偏低 2x |
| ClickUp 9.7M 月访客 | 真实 ~33M | 偏低 3x |
| Notion 142.6M 月访客 | 真实 134-170M | 准确 |
| Meta CAC $45-65 vs 行业均值 $120 | 真实 B2B SaaS CAC $200-1200+ | 严重失真 |

**模式**：10 个数据中 1 个准确、2 个大致可信、7 个有显著偏差。假精度（$87.3B、24.3%）是 LLM 幻觉的典型特征。

### Case A (Therapist) 报告对比

therapist case 的报告质量明显好于 Auxora 自身：
- 竞品选对了：BetterHelp (18.2M 月访客)、Talkspace (4.8M)、Psychology Today (42.6M)
- 市场定义精准：$77.6B U.S. Mental Health Market（需验证但量级合理）
- 竞争洞察有价值："BetterHelp 零本地 SEO"、"Psychology Today 没有在线预约功能"、"Talkspace 26% 付费流量依赖不可持续"
- 定位建议准确："高接触本地化"象限，避开风投巨头的规模竞争

---

## 三、SEO 审计：app.auxora.ai

### PageSpeed Insights 评分

| 类别 | 移动端 | 桌面端 |
|------|--------|-------|
| Performance | **57** (差) | **85** (良好) |
| Accessibility | **90** | **91** |
| Best Practices | **96** | **96** |
| SEO | **83** | **83** |

### Core Web Vitals

| 指标 | 移动端 | 桌面端 | 达标值 |
|------|--------|-------|-------|
| FCP | **8.8s** | 1.6s | < 1.8s |
| LCP | **8.8s** | 1.7s | < 2.5s |
| TBT | 0ms | 50ms | < 200ms |
| CLS | 0.007 | 0.037 | < 0.1 |

**Google 使用 mobile-first indexing，移动端 8.8 秒的 FCP/LCP 是 SEO 的真实基准。**

### 关键 SEO 问题

| 优先级 | 问题 | 影响 | 修复难度 |
|-------|------|------|---------|
| **P0** | 纯 SPA 无 SSR -- 服务器返回空 `<div id="root">` | Google 可能无法索引内容 | 高（需架构调整） |
| **P0** | 无 meta description | SERP 展示失控 | 低（10 分钟） |
| **P0** | robots.txt 返回 HTML（SPA catch-all）-- 17 处错误 | 爬虫无引导 | 低（nginx 配置） |
| **P0** | 无 sitemap.xml | Google 无法发现页面 | 低 |
| **P1** | 无 canonical 标签 | 重复内容风险 | 低 |
| **P1** | 无 OG tags | 社交分享无预览 | 低 |
| **P1** | 无 JSON-LD schema markup | 无 rich snippets | 中 |
| **P1** | Title tag 不含关键词 | 排名信号丢失 | 低 |
| **P2** | Favicon 404 | 浏览器标签无图标 | 低 |
| **P2** | 移动端 FCP/LCP 8.8s | 用户流失 + 排名惩罚 | 高（需 SSR） |
| **P2** | Footer 版权 2025 | 过时 | 低 |

### Quick Win（10 分钟内可完成，不需要架构变更）

- [ ] 添加 `<meta name="description">`
- [ ] 添加 `<link rel="canonical">`
- [ ] 添加 OG + Twitter Card tags
- [ ] nginx 配置 robots.txt 静态路由
- [ ] 生成 sitemap.xml
- [ ] 添加 favicon
- [ ] Footer 2025 → 2026

### 中期建议（需工程支持）

- [ ] SSR/Prerendering（根本解决移动端性能 + 爬虫索引问题）
- [ ] JSON-LD schema（Organization + SoftwareApplication + FAQPage）
- [ ] Code splitting + 移除未使用的 CSS/JS（节省 ~880KB）

---

## 四、Landing Page 观察

### 做得好的

- 价值主张极清晰："Your AI growth team. Done for you." + "New customers in 48 hours. Starting at $49."
- Agency vs Auxora 对比表杀伤力强（30 天/$2000+ vs 48 小时/$49）
- 6 个垂直行业分段精准（Therapists, Freelancers, Home Services, Coaches, Solo Founders, Wellness）
- 定价阶梯低门槛：Free → $4.99 → $49
- Testimonials 具体有力（Dr. Jamie R., Sarah K. 等）

### 需要注意的

- **定价不一致**：Landing page 说 "$49 launch" 和 "$200 build"，onboarding 说 "$200/月"，billing 页面说 "$50/mo Pro"。需统一对外口径
- **"28 million" vs "33 million"**：Landing page 写 28M，onboarding 写 33M。数字需统一
- **Demo 视频区域空白**：demo-poster.jpg 返回 404
- **Testimonials 真实性**：如果是真实客户应更突出；如果是构造的需替换

---

## 五、产品反馈建议（按优先级）

| 优先级 | 建议 | 原因 |
|-------|------|------|
| P0 | **GTM Report 数据需接入可验证数据源**（SimilarWeb API / 公开数据），或标注 "AI estimated" | 10 个数据中 7 个有显著偏差，损害产品可信度 |
| P0 | **SEO Quick Win 修复** -- meta description, robots.txt, sitemap, canonical | 10 分钟修复，立即改善搜索可见性 |
| P1 | **Business Profile 提取增强** -- 从 landing page 提取核心差异（定价、目标客户、卖点），不只抓 meta description 级别的泛信息 | 影响竞品选择和整个报告定位 |
| P1 | **Pipeline 状态修复** -- Interview 没做完就不显示绿勾；Research 和 Report 状态应联动 | 用户体验矛盾 |
| P2 | **定价数字统一** -- landing page / billing / onboarding 的定价需一致 | 避免用户困惑 |
| P2 | **SSR/Prerendering** -- 移动端 8.8s FCP 严重影响 SEO 和用户体验 | 长期 SEO 基础 |

---

## 六、GTM 执行计划

### 核心策略：先校准，再分发

基于 Steve Blank、Paul Graham (YC)、Superhuman PMF Engine 的框架：在 7 个客户 0% churn 的阶段，最高杠杆的动作是理解现有客户，而非铺渠道。

### Week 1: 校准（Mar 24-28）

| 任务 | 产出 |
|------|------|
| 完成 onboarding Day 1 Checklist（产品权限、体验产品、Reddit 登录、加群聊、读文档） | Checklist done |
| Hui 给客户发 warm intro，Calder 独立约时间执行 3-5 个客户访谈 | 录音 + 笔记 |
| 以 therapist 身份完整跑产品流程，记录观察 | 产品体验笔记 |
| Reddit 潜水：加入目标 sub，记录用户高频词汇和痛点 | 社区语言库 |
| 与 Tingyong/Yuhong 对齐 GA4 最小事件方案 | 事件方案文档 |
| **Friday checkpoint**：1 页 memo 给 Hui | 本周学到什么 + Week 2 建议 |

**客户访谈核心问题**（Superhuman PMF Engine 改编）：

1. 如果明天不能用 Auxora 了，你会多失望？
2. 你觉得什么样的人最适合用 Auxora？
3. Auxora 给你带来的最大好处是什么？
4. 我们怎么改进？
5. 你是怎么发现 Auxora 的？
6. 之前怎么解决营销问题？
7. 如果推荐给朋友，你会怎么说？

### Week 2: Armed Distribution（Mar 31 - Apr 6）

产品 Apr 1 上线 + 客户访谈 insight 到手。

| 任务 | 产出 |
|------|------|
| 综合访谈 + 撰写 positioning（每个垂直一套） | Customer Intelligence 文档 |
| SEO 关键词研究：客户真实语言做种子词，3 垂直 x 10 词 | Google Sheet（30 keywords） |
| 录 60s Demo 视频（产品完整版 + 客户原话写脚本） | MP4（9:16） |
| Reddit 首批 5 条高质量评论（用 validated messaging） | 5 条评论截图 |
| 确定 blog 方案 | 方案文档 |

### Week 3: Systems & Scale（Apr 7-13）

| 任务 | 产出 |
|------|------|
| Reddit 监控 Dashboard（IFTTT/Zapier） | 每天推送 5-10 条帖子 |
| 首篇 SEO 文章（角度来自客户访谈） | Published draft + URL |
| GA4 完整 dashboard（与 Tingyong/Yuhong） | GA4 上线 + Loom walkthrough |
| 视频 Pipeline 架构（条件：Week 2 demo 有正向反馈） | 架构文档 + 样例 |
| 付费实验提案：$50 Reddit ad，copy 用客户原话 | 提案文档，Hui 审批 |

### Week 4-12: Do More of What Works

不预设 checklist。每周基于数据决定。

**门控**：Reddit 没带来站内流量 → 先诊断 messaging。Blog 没就位 → 先解决。$50 测试没信号 → 不扩预算，回到 positioning。

---

## 七、首月目标（by Apr 13）

| 指标 | 目标 |
|------|------|
| 客户访谈 | 3-5 个完成 |
| Customer Intelligence 文档 | 完成，团队共享 |
| Validated positioning | 能用 1 句话说清 Auxora 对谁解决什么 |
| Reddit-sourced website visits | 可追踪（UTM） |
| SEO 文章 | 1 篇 published |
| Demo 视频 | 1 个（产品完整版） |
| GA4 | 上线 + 漏斗 dashboard |
| 付费实验提案 | Hui 审批 ready |

## 八、90 天目标

| 指标 | 目标 |
|------|------|
| 官网月流量 | 2,000+ UV |
| Reddit-sourced visits | 200+ UV/月 |
| SEO 文章 | 8-10 篇 |
| 长尾关键词前 3 页 | 5 个 |
| Case Study | 1 篇完整 |
| 核心学习 | top 2 转化 sub + top 3 关键词 + validated positioning |

---

## 九、Dependencies

| 依赖 | Owner | Deadline |
|------|-------|---------|
| Hui 给客户发 warm intro | Hui | Day 1-2 |
| SEO Quick Win 修复（meta desc, robots.txt, sitemap） | 工程团队 | 本周 |
| Apr 1 平台里程碑 | 全团队 | Apr 1 |
| Blog 方案确定 | Calder + Hui | Week 2 |
| GA4 事件方案 | Calder + Tingyong/Yuhong | Week 1 定方案, Week 3 上线 |

---

## 十、附录

### 相关文档

- `docs/plans/2026-03-24-report-auxora-dogfooding-product-review.md` -- Dogfooding 产品评测详细报告（含数据验证明细）
- `docs/plans/2026-03-24-report-auxora-seo-audit.md` -- SEO 审计完整报告（含 PageSpeed 数据）
- `docs/plans/2026-03-23-feat-auxora-gtm-final-plan.md` -- GTM 执行计划详细版

### 调研来源

- PageSpeed Insights（Lighthouse 13.0.1，移动端 + 桌面端）
- SimilarWeb / Semrush（竞品流量数据验证）
- Superhuman PMF Engine（客户访谈框架）
- Steve Blank Customer Development、Paul Graham "Do Things That Don't Scale"
- Google Search Central（people-first content 指南）
