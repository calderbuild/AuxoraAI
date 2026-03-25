---
title: Auxora.ai SEO 审计报告
type: report
date: 2026-03-24
---

# Auxora.ai SEO 审计报告

**审计目标**：https://app.auxora.ai/
**类型**：SaaS Landing Page
**审计日期**：2026-03-24

---

## Executive Summary

**整体健康度：差（需要紧急修复）**

### PageSpeed Insights 评分

| 类别 | 移动端 | 桌面端 |
|------|--------|-------|
| Performance | **57** (差) | **85** (良好) |
| Accessibility | **90** (良好) | **91** (良好) |
| Best Practices | **96** (优秀) | **96** (优秀) |
| SEO | **83** (需改进) | **83** (需改进) |

### Core Web Vitals 对比

| 指标 | 移动端 | 桌面端 | 达标值 | 移动端评级 | 桌面端评级 |
|------|--------|-------|-------|----------|----------|
| FCP | **8.8s** | **1.6s** | < 1.8s | 极差 | 通过 |
| LCP | **8.8s** | **1.7s** | < 2.5s | 极差 | 通过 |
| TBT | 0ms | 50ms | < 200ms | 通过 | 通过 |
| CLS | 0.007 | 0.037 | < 0.1 | 通过 | 通过 |
| Speed Index | **8.8s** | **2.0s** | < 3.4s | 极差 | 通过 |

**关键发现**：桌面端性能 85 分尚可（FCP 1.6s / LCP 1.7s），但**移动端性能灾难级**（FCP/LCP 均 8.8s）。原因是 SPA 纯客户端渲染 + 渲染阻塞请求在低速 4G 下放大效应严重。Google 使用 mobile-first indexing，所以**移动端的差表现才是 SEO 的真实基准**。

**最严重的 5 个问题**：

1. **纯 SPA 无 SSR** -- Google 看到的是空 HTML
2. **FCP/LCP 8.8 秒** -- 用户等 9 秒才看到内容
3. **无 meta description** -- SERP 展示完全失控
4. **无 robots.txt / sitemap.xml** -- 爬虫无引导（且 SPA catch-all 让 robots.txt 返回 HTML）
5. **无 JSON-LD schema / OG tags / canonical** -- 搜索引擎和社交平台无结构化数据

---

## Technical SEO Findings

### 1. 纯 SPA 无 SSR（Critical）

- **Issue**：服务器返回的 HTML 只有 `<div id="root"></div>`，所有内容靠 JS 渲染
- **Impact**：**Critical** -- Googlebot 需要二次渲染才能看到内容，可能延迟数天到数周。新页面可能根本不被索引
- **Evidence**：`curl -s https://app.auxora.ai/ | grep -c "root"` 确认 HTML body 只有一个空 div
- **Fix**：迁移到 Next.js SSR/SSG，或至少为 landing page 添加 prerendering（如 Prerender.io）

### 2. robots.txt 不存在（High）

- **Issue**：`/robots.txt` 返回 SPA 的 index.html（因为 catch-all routing），不是有效的 robots.txt 文件。PageSpeed 检测到 17 处 robots.txt 错误
- **Impact**：**High** -- 爬虫无法获取抓取规则，无 sitemap 引用
- **Evidence**：`curl -s https://app.auxora.ai/robots.txt` 返回 HTML 而非纯文本
- **Fix**：在 nginx 配置中为 `/robots.txt` 添加静态文件路由，内容示例：
  ```
  User-agent: *
  Allow: /
  Sitemap: https://app.auxora.ai/sitemap.xml
  ```

### 3. sitemap.xml 不存在（High）

- **Issue**：`/sitemap.xml` 同样返回 SPA index.html
- **Impact**：**High** -- Google 无法发现所有可索引的页面
- **Fix**：生成静态 sitemap.xml，包含所有公开页面 URL（landing page、/report、/privacy、/terms）

### 4. Canonical 标签缺失（High）

- **Issue**：页面无 `<link rel="canonical">` 标签
- **Impact**：**High** -- 如果有多个 URL 指向同一内容（如 trailing slash 差异），Google 无法判断首选版本
- **Evidence**：Playwright `document.querySelector('link[rel="canonical"]')` 返回 null
- **Fix**：添加自引用 canonical `<link rel="canonical" href="https://app.auxora.ai/" />`

### 5. Favicon 缺失（Low）

- **Issue**：无 favicon 定义，`/favicon.ico` 返回 404
- **Impact**：**Low** -- 浏览器标签和搜索结果中无图标
- **Fix**：添加 favicon 文件 + `<link rel="icon" href="/favicon.ico">`

### 6. FCP/LCP 8.8 秒（Critical）

- **Issue**：首次内容渲染和最大内容渲染都要 8.8 秒（移动端模拟）
- **Impact**：**Critical** -- 用户可能在内容加载前离开；Google 将此作为排名信号
- **Evidence**：PageSpeed Insights 移动端测试
- **Root Cause**：SPA 纯客户端渲染 + 渲染阻塞请求（预计可缩短 4,360ms）+ 未使用的 JS/CSS（可节省 534KB JS + 347KB CSS）
- **Fix**：
  - 迁移 SSR 是根本解决方案
  - 短期：code splitting、tree shaking、延迟加载非首屏内容
  - 移除未使用的 FontAwesome CSS（整个库加载只用了几个图标）

### 7. 缓存策略不足（Medium）

- **Issue**：可节省 9,993 KiB 的缓存
- **Impact**：**Medium** -- 回访用户加载慢
- **Fix**：为静态资源设置长期 Cache-Control 头（JS/CSS 已有 hash 文件名，可设 1 年缓存）

### 8. 安全 Header 缺失（Medium）

- **Issue**：无 HSTS、无 CSP、无 XFO（X-Frame-Options）、无 COOP
- **Impact**：**Medium** -- 安全最佳实践未达标
- **Fix**：在 nginx 中添加安全响应头

---

## On-Page SEO Findings

### 9. Meta Description 缺失（Critical）

- **Issue**：页面无 `<meta name="description">` 标签
- **Impact**：**Critical** -- Google 会自动从页面内容抓取摘要，结果不可控；CTR 损失严重
- **Fix**：添加 150-160 字符的 meta description，例如：
  ```
  Auxora is the AI marketing engine for one-person businesses. Get a complete marketing stack — ads, landing pages, SEO, emails — live in 48 hours. From $49.
  ```

### 10. Title Tag 不含关键词（Medium）

- **Issue**：当前标题 "Auxora -- AI Growth OS"。不含任何目标关键词（如 "AI marketing for solopreneurs" 或 "marketing for one-person business"）
- **Impact**：**Medium** -- 标题是最重要的 on-page SEO 信号
- **Fix**：改为包含关键词的标题，例如：
  ```
  Auxora — AI Marketing for One-Person Businesses | Ads, SEO & Landing Pages in 48 Hours
  ```

### 11. OG Tags 完全缺失（Medium）

- **Issue**：无任何 Open Graph 标签（og:title、og:description、og:image）
- **Impact**：**Medium** -- 在 Twitter、LinkedIn、Facebook 分享时无法控制预览显示
- **Fix**：添加完整 OG + Twitter Card 标签

### 12. H1 标签内容（Low -- 已良好）

- **Issue**：H1 是 "Your AI growth team. Done for you." -- 有说服力但不含搜索关键词
- **Impact**：**Low** -- 对转化好，对 SEO 可优化
- **Fix**：可接受保持现状（H1 侧重转化），通过 H2 和正文内容覆盖关键词

### 13. JSON-LD Schema Markup 缺失（Medium）

- **Issue**：页面无任何结构化数据
- **Impact**：**Medium** -- 无 rich snippets 机会（FAQ、SoftwareApplication、Organization）
- **Evidence**：Playwright `document.querySelectorAll('script[type="application/ld+json"]')` 返回空数组
- **Fix**：添加以下 schema：
  - `Organization`（公司信息）
  - `SoftwareApplication`（产品信息 + 定价）
  - `FAQPage`（FAQ section 已有 8 个问题，天然适合）

### 14. 图片优化（Low -- 基本通过）

- **Issue**：页面只有 1 张图片（logo），有 alt text
- **Impact**：**Low** -- 当前图片很少，问题不大
- **Fix**：确保后续添加的图片都有描述性 alt text + WebP 格式

---

## Accessibility Findings

PageSpeed 得分 90（良好），但有以下问题：

| 问题 | 严重度 |
|------|-------|
| 背景色和前景色对比度不足 | Medium |
| 触摸目标尺寸或间距不足 | Medium |
| 文档缺少主要 landmark（main） | Low |
| 标题元素未按降序排列 | Low |
| Video 元素缺少字幕 track | Low |

---

## Content Quality Assessment

### E-E-A-T 信号

| 信号 | 状态 | 改进建议 |
|------|------|---------|
| Experience | 有真实客户案例（4 条 testimonials） | 需确认是否为真实客户 |
| Expertise | 产品定位清晰，行业痛点描述准确 | 缺少团队/创始人介绍 |
| Authority | 无外部引用、无 backlink | 需要通过内容和 PR 建立 |
| Trust | 有 Privacy/Terms 页面，HTTPS，contact email | 缺少公司地址、团队页面 |

### Landing Page 内容质量

**做得好的**：
- 痛点描述精准（"Meta & Google ads feel like a black box"）
- Agency vs Auxora 对比表直观有力
- 6 个垂直行业分段精准
- 定价透明（Free → $4.99 → $49）
- FAQ 覆盖常见问题

**需要改进的**：
- 没有 blog（SEO 内容基建为零）
- 没有独立的行业页面（/ai-marketing-for-therapists 等 -- programmatic SEO 机会）
- 没有对比页面（/auxora-vs-jasper 等）
- Footer 版权年份写的 2025

---

## Prioritized Action Plan

### P0: Critical（阻断索引/排名，应本周解决）

1. **添加 meta description** -- 10 分钟修复，立即改善 SERP 展示
2. **添加静态 robots.txt** -- nginx 配置加一个 location block
3. **添加静态 sitemap.xml** -- 列出所有公开 URL
4. **添加 canonical 标签** -- `<link rel="canonical">`
5. **添加 OG tags** -- 控制社交分享预览

### P1: High（对排名有显著影响，应两周内解决）

6. **优化 Title tag** -- 加入目标关键词
7. **添加 JSON-LD schema** -- Organization + SoftwareApplication + FAQPage
8. **SSR/Prerendering** -- 至少为 landing page 做预渲染（Prerender.io 或 Next.js 迁移）
9. **性能优化** -- code splitting 减少首屏 JS、移除未用 CSS/FontAwesome

### P2: Medium（持续改进）

10. **添加 favicon**
11. **安全 headers**（HSTS、CSP、XFO）
12. **缓存策略优化**
13. **无障碍**：对比度修复、触摸目标调大
14. **Footer 年份** 2025 → 2026

### P3: 长期 SEO 建设

15. **建 blog** -- 每周 1 篇 SEO 文章
16. **行业垂直页** -- /ai-marketing-for-therapists 等 programmatic SEO
17. **对比页** -- /auxora-vs-jasper 等截流内容
18. **提交 Google Search Console** -- 监控索引和排名

---

## Quick Win 清单（10 分钟内可完成）

这些都是纯前端/配置改动，不需要架构变更：

- [ ] 添加 `<meta name="description" content="...">`
- [ ] 添加 `<link rel="canonical" href="https://app.auxora.ai/">`
- [ ] 添加 OG tags（og:title, og:description, og:image, og:url）
- [ ] 添加 Twitter Card tags
- [ ] nginx 配置 robots.txt 静态路由
- [ ] 生成 sitemap.xml 静态文件
- [ ] 添加 favicon
- [ ] 修复 Footer 年份 2025 → 2026

---

## 数据来源

- PageSpeed Insights API（移动端，Lighthouse 13.0.1）
- Playwright 浏览器渲染检测（schema、meta tags、headings）
- curl HTTP headers 检查
- HTML 源码分析
