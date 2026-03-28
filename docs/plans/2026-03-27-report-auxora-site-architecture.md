---
title: Auxora.ai 整站 URL 架构诊断与重构建议
type: report
date: 2026-03-27
author: Calder
audience: Hui Li (CEO), 工程团队
---

## 结论

Auxora 当前只有 5 个可工作的路由，营销站和应用混部在 `app.auxora.ai` 上，首页 5 个 CTA 指向的 `/report` 路由不工作。没有 404 页面、没有 robots.txt、没有 sitemap.xml，对搜索引擎完全不可见。

## 一、当前 URL 清单与路由状态

| 路由 | 实际行为 | HTTP 状态 | 备注 |
|------|---------|-----------|------|
| `auxora.ai/*` | 301 -> `app.auxora.ai/*` | 301 | 所有路径均重定向 |
| `/` | 正常渲染首页 | 200 | 唯一的营销页面 |
| `/login` | 登录页 | 200 | 正常 |
| `/login?mode=signup` | 注册页 | 200 | 共用 `/login` 路由，query param 切换 |
| `/privacy` | 隐私政策页 | 200 | 正常，有独立导航和 footer |
| `/terms` | 服务条款页 | 200 | 正常，有独立导航和 footer |
| `/report` | **静默回退到首页** | 200 | 首页 5 个 CTA 指向此路由 |
| `/dashboard` | 重定向到 `/login` | 200 | 需要认证，符合预期 |
| `/new` | 重定向到 `/login` | 200 | 需要认证，符合预期 |
| `/workspace` | 回退到首页 | 200 | 首页 demo 区域提及但无公开路由 |
| `/pricing` | 回退到首页 | 200 | 不存在，首页 nav 用 `#pricing` 锚点 |
| `/about` | 回退到首页 | 200 | 不存在 |
| `/blog` | 回退到首页 | 200 | 不存在 |
| `/sitemap.xml` | 返回 SPA 空壳 HTML | 200 | 不存在 |
| `/robots.txt` | 返回 SPA 空壳 HTML | 200 | 不存在 |
| 任意无效路径 | 回退到首页 | 200 | 无 404 页面 |

关键发现：nginx 对所有路由返回同一份 906 字节的 SPA 空壳 HTML（`200 OK`），前端 router 决定渲染内容。不识别的路由静默回退首页，无任何用户提示。

## 二、域名架构问题

**现状**：`auxora.ai` 301 -> `app.auxora.ai`，营销站和应用共用一个域名。

**问题**：
1. 营销页面的 canonical URL 变成 `app.auxora.ai`，SEO 信号全部分散到应用域名上
2. 搜索引擎无法区分哪些页面应被索引（营销页）、哪些不该索引（`/dashboard`）
3. 应用的 auth 逻辑（401 错误）影响爬虫对公开页面的抓取

**建议分离方案**：

| 域名 | 用途 | 内容 |
|------|------|------|
| `auxora.ai` | 营销站（SEO 主域） | 首页、行业页、定价、博客、/report 入口 |
| `app.auxora.ai` | 应用 | /login、/dashboard、/workspace、/new |

短期（4/1 前）不必物理分离，但必须在 `app.auxora.ai` 上修复 robots.txt，区分可索引和不可索引页面。

## 三、建议的目标 URL 层级

```
auxora.ai/                          # 首页（营销主页）
  |-- /pricing                      # 独立定价页（从首页锚点升级）
  |-- /report                       # 免费报告入口（修复断裂路由）
  |-- /for/
  |     |-- /therapists             # 行业着陆页
  |     |-- /consultants
  |     |-- /home-services
  |     |-- /coaches
  |     |-- /solo-founders
  |     +-- /wellness
  |-- /blog/                        # SEO 内容中心
  |     +-- /blog/:slug
  |-- /about                        # 公司介绍
  |-- /privacy                      # 保留
  |-- /terms                        # 保留
  +-- /404                          # 自定义 404 页面

app.auxora.ai/                      # 应用（不索引）
  |-- /login
  |-- /login?mode=signup
  |-- /dashboard
  |-- /workspace
  +-- /new
```

## 四、新增页面优先级

| 优先级 | 页面 | 理由 |
|--------|------|------|
| P0 -- 4/1 前 | 修复 `/report` | 首页 5 个 CTA 全部断裂，直接影响转化 |
| P0 -- 4/1 前 | `robots.txt` + `sitemap.xml` | SEO 基础设施，当前对搜索引擎完全不可见 |
| P0 -- 4/1 前 | 自定义 404 页面 | 当前所有无效 URL 静默回退首页，用户和爬虫都困惑 |
| P1 -- 4 月 | `/for/therapists` 等行业页 | 首页 footer 5 个行业链接全指向同一个锚点，SEO 价值为零 |
| P1 -- 4 月 | 独立 `/pricing` | 当前只有锚点，无法被搜索引擎独立索引和排名 |
| P2 -- Q2 | `/blog` | 长尾关键词入口，organic 流量的主要渠道 |
| P2 -- Q2 | `/about` | 建立品牌信任，B2B 决策参考 |

## 五、SEO URL 规范

1. **Canonical 标签**：每个公开页面必须有 `<link rel="canonical">`，统一到 `auxora.ai`（不带 `app.` 前缀）
2. **Slug 命名**：小写、连字符分隔、纯英文（`/for/home-services` 而非 `/for/HomeServices`）
3. **内链结构**：首页 footer 的行业链接应指向各自独立页面（`/for/therapists`），不应全部指向 `#who-its-for`
4. **robots.txt 内容**：

```
User-agent: *
Allow: /
Disallow: /dashboard
Disallow: /workspace
Disallow: /new
Disallow: /login
Sitemap: https://auxora.ai/sitemap.xml
```

5. **sitemap.xml 应包含**：

```
/                     -- priority: 1.0, changefreq: weekly
/pricing              -- priority: 0.8
/report               -- priority: 0.8
/for/therapists       -- priority: 0.7
/for/consultants      -- priority: 0.7
/for/home-services    -- priority: 0.7
/for/coaches          -- priority: 0.7
/for/solo-founders    -- priority: 0.7
/for/wellness         -- priority: 0.7
/privacy              -- priority: 0.3
/terms                -- priority: 0.3
```

6. **Server-side 修复**：nginx 必须对 `/robots.txt` 和 `/sitemap.xml` 返回正确的 `Content-Type`（`text/plain` / `application/xml`），而非 SPA 的 `text/html`

## 六、其他发现

- Footer 版权显示 "2025"，应更新为 "2026"
- Privacy 页和 Terms 页的 footer 与首页 footer 结构不同（缺少行业链接），应统一
- Privacy 页联系邮箱为 `academy@auxora.ai`，首页为 `hello@auxora.ai`，不一致
- 首页 demo 区域显示 `app.auxora.ai/workspace` 但该路由对未登录用户不可达
