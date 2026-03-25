---
title: Week 1 收尾 + Week 2 预备：基于今日调研的行动计划
type: feat
date: 2026-03-24
---

# Week 1 收尾 + Week 2 预备

## 今日学到了什么（Mar 24）

两份报告（Dogfooding + SEO 审计）给 Week 2 分发提供了关键约束：

**Dogfooding 核心发现**
- GTM Report 数据可信度严重不足：10 个数字中 7 个有显重偏差或疑似虚构
- 流程体验好（URL → 报告 5 分钟），但报告内容不可作为 GTM 内容的引用来源
- 产品 Landing Page 的销售力强，痛点 + 对比表 + 定价阶梯逻辑清晰
- P0 问题需在 standup 或 Hui 1:1 中提出：数据准确性、竞品选择逻辑

**SEO 审计核心发现**
- 移动端 FCP/LCP 均 8.8 秒：纯 SPA 无 SSR，Googlebot 看到空 HTML
- 无 meta description / robots.txt / sitemap / JSON-LD：基础 SEO 配置缺失
- Quick wins（10 分钟内）：meta description、canonical、OG tags、robots.txt 静态路由
- 根本修复需要 Next.js SSR 迁移或 prerendering，是工程侧的决策

---

## Mar 25-28：Week 1 剩余任务

| 任务 | 产出 | 说明 |
|------|------|------|
| 向 Hui 汇报 Dogfooding P0 问题 | Slack 消息或 1:1 议题 | 数据准确性是产品信任的根基，需要工程排期 |
| 向 Hui 汇报 SEO Quick Wins | SEO Quick Win 清单 | 纯配置改动，工程 30 分钟内可修；SSR 迁移是更大决策，供 Hui 权衡 |
| 跟进客户访谈 warm intro | Hui 发出 intro 后 Calder 约时间 | 当前阻塞：需要 Hui 先发 warm intro |
| Reddit 潜水：therapist / pest control / freelance 相关 sub | 社区语言库（spreadsheet）| 记录用户如何描述问题，为 Week 2 messaging 提供种子词 |
| GA4 最小事件方案与 Tingyong/Yuhong 对齐 | 事件方案确认 | sign_up / generate_lead / purchase 三个事件 |
| Friday Memo 给 Hui | 1 页 memo | 本周学到什么 + Week 2 优先级提议 |

### Reddit 潜水目标 sub（立即可开始）

- r/therapists、r/privatepractice
- r/pestcontrol
- r/freelance、r/consulting
- r/smallbusiness、r/solopreneur

观察维度：用户如何描述营销痛点、用什么词汇描述竞争对手（agency / DIY / BetterHelp 等）、什么触发了他们寻找解决方案。记录原话，不要翻译或抽象。

---

## Friday Memo 框架（Mar 28）

给 Hui 的 1 页 memo，结构：

1. **本周完成**：Dogfooding 报告 + SEO 审计 + Reddit 潜水（X 条帖子读完，Y 个高频词汇）
2. **关键发现**：GTM Report 数据可信度问题（P0）、SEO 基础配置缺失（Quick Wins 可立即执行）、客户语言初步观察
3. **需要 Hui 决策的 3 件事**：
   - Dogfooding P0：数据准确性修复排进工程 backlog 了吗？
   - SEO Quick Wins：谁来执行，什么时候？
   - 客户访谈 warm intro：本周发出了吗？还有哪些客户可以联系？
4. **Week 2 优先级提议**：客户访谈（最高）→ Reddit 首批评论（用本周积累的语言）→ 关键词研究（以客户原话为种子词）

---

## 对 Week 2 分发的约束

基于今日两份报告，Week 2 的 Reddit 评论和内容需要注意：

- **不引用 Auxora GTM Report 里的具体数字**（可信度未验证），聚焦流程价值（"5 分钟出报告"）
- **SEO 文章不急于发布**，等工程侧完成 meta description + OG tags 等基础配置后再推，否则文章无法被正常索引和社交分享
- **Demo 视频脚本**：等产品 Apr 1 完整上线后再录，避免功能变化导致视频过时
- **Reddit 评论内容来源**：必须来自客户访谈原话或社区观察的真实语言，不用 AI 报告里的数据
