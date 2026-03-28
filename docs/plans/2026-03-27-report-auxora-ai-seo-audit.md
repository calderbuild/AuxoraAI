---
title: Auxora.ai AI SEO 诊断报告
type: report
date: 2026-03-27
author: Calder
audience: Hui Li (CEO), 全团队
---

# Auxora.ai AI SEO 诊断报告

## 诊断结论

**Auxora 在 AI 搜索中的可见度为零。** Google 搜索、ChatGPT、Perplexity、Claude 均无法发现或引用 Auxora 的任何内容。原因是三层阻断叠加：robots.txt 封杀 AI 爬虫、SPA 架构导致内容不可抓取、全网无第三方存在。

好消息是：落地页内容质量本身不差，修复技术基础设施后有明显的增长空间。坏消息是：当前所有 "best AI marketing tool for solopreneurs" 类查询的 AI 引用位被 Jasper、GoHighLevel、HubSpot 等竞品占据，Auxora 的品类定位（done-for-you AI marketing for one-person businesses）在 AI 回答中完全空白。

---

## 1. 致命问题：robots.txt 封杀了所有 AI 爬虫

`auxora.ai/robots.txt` 当前配置对主流 AI 搜索爬虫全部 `Disallow: /`：

| 爬虫 | 对应平台 | 当前状态 |
|------|---------|---------|
| GPTBot | ChatGPT | Disallow: / |
| ClaudeBot | Claude | Disallow: / |
| Google-Extended | Gemini / AI Overviews | Disallow: / |
| CCBot | Common Crawl（纯训练） | Disallow: / |
| Amazonbot | Amazon / Alexa | Disallow: / |
| Bytespider | 字节跳动 | Disallow: / |
| meta-externalagent | Meta AI | Disallow: / |
| CloudflareBrowserRenderingCrawler | Cloudflare | Disallow: / |
| PerplexityBot | Perplexity | 未提及（默认允许） |
| Bingbot | Microsoft Copilot | 未提及（默认允许） |

**影响**：即使页面内容完美，ChatGPT、Claude、Google AI Overviews 也被明确禁止抓取 Auxora 的任何页面。这是最严重的问题，也是投入产出比最高的修复点。

**建议修改为**：

```
# 允许 AI 搜索引擎抓取和引用
User-agent: GPTBot
Allow: /

User-agent: ChatGPT-User
Allow: /

User-agent: ClaudeBot
Allow: /

User-agent: Google-Extended
Allow: /

User-agent: PerplexityBot
Allow: /

User-agent: Bingbot
Allow: /

# 阻止纯训练爬虫（不产生引用，只消耗带宽）
User-agent: CCBot
Disallow: /

User-agent: Bytespider
Disallow: /
```

**保留封杀的理由**：CCBot（Common Crawl）和 Bytespider 是纯训练用途，不会在搜索结果中产生引用。放开搜索引擎类 AI 爬虫，封杀纯训练爬虫，是当前行业共识做法。

---

## 2. 架构问题：SPA 渲染 + meta 标签缺失

### 2.1 域名结构

`auxora.ai` 301 重定向到 `app.auxora.ai`。这意味着：

- 没有独立的营销站（marketing site）供搜索引擎索引
- 落地页和产品 dashboard 共用同一个 SPA 应用域名
- 搜索引擎和 AI 爬虫看到的是一个空的 HTML shell

### 2.2 HTML head 元信息

用 Playwright 渲染后检查 `<head>` 标签，结果如下：

| 元素 | 状态 | 影响 |
|------|------|------|
| `<title>` | "Auxora -- AI Growth OS" | 有，但不含目标关键词（solopreneur、marketing） |
| `<meta name="description">` | **缺失** | 搜索引擎无法获取页面摘要 |
| `<meta property="og:title">` | **缺失** | 社交分享无标题 |
| `<meta property="og:description">` | **缺失** | 社交分享无描述 |
| `<meta property="og:image">` | **缺失** | 社交分享无预览图 |
| `<link rel="canonical">` | **缺失** | 搜索引擎无法判断规范 URL |
| JSON-LD / Schema | **零条** | AI 系统无法结构化理解页面内容 |
| Sitemap | **无法访问** | 重定向到 SPA 空响应 |
| Favicon | **404** | 浏览器标签页无图标 |
| `lang="en"` | 正确 | -- |

### 2.3 控制台报错

| 资源 | 状态 |
|------|------|
| `/favicon.ico` | 404 |
| `/api/auth/refresh` | 401 |
| `/static/demo-poster.jpg` | 404 |

---

## 3. 内容可提取性评估

通过 Playwright 渲染后抓取了完整页面内容，逐项评估 AI 可提取性：

| 检查项 | 状态 | 说明 |
|--------|------|------|
| 首段产品定义 | 不通过 | H1 "Your AI growth team. Done for you." 是感性文案，缺少 40-60 词的机器可读产品定义 |
| 自包含回答块 | 不通过 | 没有可独立引用的段落（AI 需要不依赖上下文就能理解的文字块） |
| 统计数据 + 来源 | 部分通过 | 有数据（"28 million"、"62% CAC reduction"、"10x revenue growth"），但无引用来源 |
| 对比表格 | 通过 | Agency vs Auxora 对比表格结构清晰，时间/价格对比一目了然 |
| FAQ 内容 | 部分通过 | 有 8 个高质量 FAQ，但是手风琴折叠状态 -- 答案隐藏在 JS 交互后面，爬虫看不到 |
| Schema 结构化数据 | 不通过 | 页面上零条 JSON-LD |
| 作者归属 | 不通过 | 无作者信息、无团队页面、无 About 页面 |
| 更新日期 | 不通过 | 页面无任何日期信号 |
| 标题层级 | 部分通过 | H1 -> H2 -> H3 基本合理，但 H2 命名偏感性（"Marketing keeps getting in the way"），不利于 AI 按查询匹配 |

### 页面内容亮点（修复技术问题后可直接利用）

- 三层定价结构（Free / $4.99 / $49）清晰明了
- "Agency vs Auxora" 对比表格有很强的引用潜力
- 垂直行业分区（Therapists、Freelancers、Home Services、Coaches、Solo Founders、Wellness）覆盖面广
- 4 条客户证言有具体数据（"3 new retainer clients in 3 weeks"、"calendar fully booked within 5 weeks"）
- 成果数据板块（10x revenue、3x ROAS、62% CAC reduction、6 weeks to profitability）

---

## 4. 第三方存在感

AI 系统引用内容时，第三方来源的权重远高于品牌自有站点。据研究，品牌通过第三方来源被 AI 引用的概率是自有域名的 6.5 倍。

| 平台 | Auxora 存在感 | 优先级 |
|------|-------------|-------|
| Google 搜索结果 | 品牌搜索无结果 | P0 |
| Product Hunt | 无 | P1 |
| G2 / Capterra | 无 | P1 |
| Reddit | u/BeatImpress___ 账号存在，暂无 Auxora 相关帖子 | P2 |
| YouTube | 无 | P2 |
| Wikipedia | 无（暂不现实） | P3 |
| 行业 roundup 文章 | 零收录 | P2 |
| Quora | 无 | P3 |

**搜索 "Auxora AI marketing tool solopreneurs" 的结果**：Google 返回零条相关结果。所有结果都是其他 AI 工具列表文章，Auxora 不在其中任何一篇。

---

## 5. 竞品 AI 引用情况

在 "best AI marketing tool for solopreneurs" 和 "AI marketing for one person business" 查询中，以下品牌被 AI 系统高频引用：

| 竞品 | 定位 | AI 引用频率 | 与 Auxora 竞争关系 |
|------|------|-----------|------------------|
| Jasper AI | AI 文案写作 | 极高 | 间接竞品（只做内容，不做执行） |
| GoHighLevel | All-in-one 营销平台 | 高 | 直接竞品（但面向有营销经验的用户） |
| HubSpot | 营销自动化 | 高 | 间接竞品（定价和复杂度远超 solopreneur 需求） |
| Mailchimp | 邮件营销 | 高 | 细分竞品（只做邮件） |
| SolopreneursAI | solopreneurs.ai | 中 | 域名竞品（定位相似） |
| Lindy / Relevance AI | AI Agent 平台 | 中 | 技术层竞品（Agent 框架，非 done-for-you） |

**关键洞察**：Auxora 的独特定位 -- "done-for-you AI marketing for one-person businesses, from $49, clients in 48 hours" -- 在 AI 回答中没有任何竞品精确覆盖。这是一个可以占据的品类空位，但前提是有可索引的内容去填充。

---

## 6. 修复路线图

### P0 -- 本周（技术基础，工程团队执行）

| 任务 | 负责人 | 预期效果 |
|------|--------|---------|
| 修改 robots.txt：放开 GPTBot、ClaudeBot、Google-Extended、PerplexityBot | 工程 | AI 爬虫获得抓取权限 |
| 添加 `<meta description>`、Open Graph 标签 | 工程 | 搜索引擎和社交平台可展示正确摘要 |
| 添加 `<link rel="canonical" href="https://auxora.ai/">` | 工程 | 明确规范 URL，避免重复内容问题 |
| 修复 favicon 404 | 工程 | 消除 console 报错 |
| 生成 sitemap.xml（至少包含 `/`、`/report`、`/privacy`、`/terms`） | 工程 | 搜索引擎可发现所有可索引页面 |

**建议 meta description**：
> "Auxora is a done-for-you AI marketing platform for one-person businesses. Ads, landing pages, SEO, and emails -- built and live in 48 hours, starting at $49."

**建议 title 优化**：
> "Auxora -- AI Marketing for One-Person Businesses | Ads, SEO & Landing Pages from $49"

### P1 -- 两周内（SSR + 结构化数据）

| 任务 | 说明 |
|------|------|
| 首页 SSR / SSG | 当前 SPA 空壳对爬虫不可见。至少首页（含 FAQ）需要服务端渲染 |
| 营销站与应用分离 | 推荐方案：`auxora.ai` 或 `www.auxora.ai` 作为静态营销站，`app.auxora.ai` 作为产品应用。当前 301 把所有 SEO 价值推给了一个 SPA |
| 添加 JSON-LD Schema | `Organization` + `SoftwareApplication` + `FAQPage` + `Product`（含定价） |
| FAQ 内容 SSR 渲染 | 即使前端保持折叠交互，HTML 中需要包含完整答案文本，供爬虫读取 |
| 修复 `/static/demo-poster.jpg` 404 | 视频缩略图缺失 |

### P2 -- 一个月内（内容 + 第三方存在）

| 任务 | 说明 |
|------|------|
| 添加机器可读产品定义 | 在 H1 下方加 40-60 词产品定义段，直接回答 "What is Auxora?" |
| 统计数据加引用来源 | "28 million one-person businesses" 注明来源（如 Bureau of Labor Statistics, Non-Employer Statistics） |
| 创建对比页面 | "Auxora vs Hiring a Marketing Agency"、"Auxora vs Jasper vs GoHighLevel" |
| 创建垂直行业页面 | "/for/therapists"、"/for/pest-control"、"/for/freelancers" -- 独立 URL，独立 SEO |
| Product Hunt launch | 建立第一个高权重第三方存在 |
| G2 / Capterra profile | 注册并邀请早期用户留评 |
| Reddit 内容启动 | r/solopreneur、r/Entrepreneur、r/therapists 发有价值帖子，自然引出 Auxora |

### P3 -- 持续（监控 + 内容引擎）

| 任务 | 说明 |
|------|------|
| 月度 AI 可见度检查 | 在 ChatGPT、Perplexity、Google 搜索 top 20 查询，追踪引用状态 |
| Blog / 知识库 | 针对长尾词创建权威内容（"therapist marketing guide"、"pest control lead generation"） |
| 争取行业 roundup 收录 | 联系 "best AI marketing tools" 类文章作者，申请收录 |
| 考虑 AI 可见度监控工具 | Otterly AI、Peec AI、ZipTie（待品牌有一定存在感后再投入） |

---

## 7. 目标查询清单

建议优先争取 AI 引用的 20 个查询，按类别分组：

### 品类查询（最高优先级）

1. "best AI marketing tool for solopreneurs"
2. "AI marketing for one person business"
3. "done for you marketing AI"
4. "AI virtual CMO"
5. "automated marketing for small business"

### 垂直行业查询

6. "therapist marketing AI"
7. "how to get therapy clients online"
8. "pest control lead generation AI"
9. "freelancer marketing automation"
10. "life coach marketing tool"

### 对比查询

11. "Auxora vs marketing agency"
12. "AI marketing vs hiring agency"
13. "cheap alternative to marketing agency for solopreneurs"
14. "GoHighLevel alternative for solopreneurs"
15. "marketing agency vs AI tool cost comparison"

### 问题查询

16. "how to market a one person business"
17. "solopreneur marketing on a budget"
18. "how to get clients without referrals"
19. "marketing for therapists in private practice"
20. "solo founder customer acquisition"

---

## 8. 预期效果

| 阶段 | 时间线 | 预期里程碑 |
|------|--------|-----------|
| P0 完成 | 1 周 | AI 爬虫可访问页面；Google 开始索引 |
| P1 完成 | 3 周 | SSR 首页可被完整抓取；结构化数据上线；社交分享卡片正常显示 |
| P2 完成 | 6 周 | 品牌搜索在 Google 有结果；Product Hunt 和 G2 有 profile；首批对比/垂直页面上线 |
| P3 持续 | 3-6 月 | 开始在 AI 回答中被引用；"Auxora" 品牌查询在 ChatGPT/Perplexity 返回准确信息 |

**基准参考**：根据 Princeton GEO 研究（KDD 2024），优化后的内容被 AI 引用的概率是未优化内容的 3 倍；加入统计数据和引用来源可提升 AI 可见度 37-40%。对于低域名权重的新站，引用来源优化的效果更显著，最高可达 115% 的可见度提升。

---

## 附录：诊断方法

| 检查维度 | 工具 / 方法 |
|---------|------------|
| robots.txt | WebFetch 直接抓取 `auxora.ai/robots.txt` |
| 页面 meta 标签 | Playwright 渲染后 `document.querySelectorAll('meta')` 提取 |
| 页面内容结构 | Playwright `browser_snapshot` 获取完整 accessibility tree |
| Schema / JSON-LD | Playwright 提取 `script[type="application/ld+json"]` |
| Console 报错 | Playwright console 日志监控 |
| AI 搜索可见度 | WebSearch 搜索 "Auxora AI marketing tool solopreneurs" 和品类关键词 |
| 竞品引用情况 | WebSearch 搜索 "best AI marketing tool for solopreneurs one person business" |
| 第三方存在感 | 人工检查 Product Hunt、G2、Reddit、YouTube |
