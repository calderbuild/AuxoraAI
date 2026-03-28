---
title: Auxora.ai 页面转化率诊断报告
type: report
date: 2026-03-27
author: Calder
audience: Hui Li (CEO), 全团队
---

# Auxora.ai 页面转化率（CRO）诊断报告

## 诊断结论

首页的文案质量和信息密度在同类产品中属于上乘，但**转化漏斗存在结构性瓶颈**：核心转化路径混乱（3 个不同入口指向不同目标）、定价信息自相矛盾（首页至少出现 3 套价格）、"Get started" 直接跳登录页形成断崖式流失。以下是逐层诊断。

---

## 1. 转化漏斗结构分析

### 1.1 当前页面清单

| 页面 | URL | 状态 |
|------|-----|------|
| 首页（营销页） | app.auxora.ai/ | 正常，内容丰富 |
| 登录页 | app.auxora.ai/login | 正常 |
| 注册页 | app.auxora.ai/login（切换态） | 正常 |
| Report 页 | app.auxora.ai/report | **失败 -- 回退到首页** |
| Dashboard | app.auxora.ai/dashboard | 重定向到 /login |
| Privacy / Terms | app.auxora.ai/privacy, /terms | 未检查 |

**致命发现**：`/report` 路由不生效，访问后回退到首页。首页上有多个 CTA 指向 `/report`（"Get my free snapshot"、"Get my strategy report"、"Get your full report"），**全部失效**。这意味着当前最核心的免费获客入口完全断裂。

### 1.2 CTA 路径分析

首页有**三条并行转化路径**，导致用户选择困难：

| CTA 文案 | 指向 | 出现位置 | 问题 |
|---------|------|---------|------|
| "Get New Customers in 48 Hours" | #early-access（页底邮件表单） | Hero 区 | 主 CTA，但跳到页底体验断裂 |
| "Get started ->" | /dashboard -> /login | 导航栏 | 直接进登录页，无过渡，冷访客直接流失 |
| "Get my free snapshot" | /report | 定价卡 Free 层 | **路由失效，回退首页** |
| "Get my strategy report" | /report | 定价卡 $4.99 层 | **路由失效，回退首页** |
| "Get new customers in 48 hours" | #early-access | 定价卡 $49 层 | 又回到页底表单 |
| "Get More Revenue" | #early-access | 导航栏 + 页底 | 重复路径 |

**核心问题**：一个冷访客到达首页后，不知道该点哪个按钮。三条路径分别对应三个不同动作（留邮箱、去注册、去看报告），但视觉层级几乎相同。

---

## 2. Hero 区诊断

![首页全貌（桌面端）](https://raw.githubusercontent.com/calderbuild/AuxoraAI/main/docs/screenshots/auxora-homepage-full.png)

### 2.1 5 秒测试

| 维度 | 评分 | 说明 |
|------|------|------|
| 是什么 | 7/10 | "Your AI growth team. Done for you." -- 大方向清楚，但 "growth team" 概念模糊 |
| 给谁用 | 9/10 | "Built for one-person businesses" -- 非常清晰 |
| 为什么选我 | 8/10 | "New customers in 48 hours. Starting at $49." -- 有力 |
| 下一步做什么 | 5/10 | 导航栏两个按钮 + Hero 一个大按钮，三者指向不同位置 |

### 2.2 Hero 区具体问题

**问题 1：CTA 目标混乱**

- 导航栏 "Get More Revenue" -> 跳到页底 #early-access
- 导航栏 "Get started" -> 直接跳 /login
- Hero "Get New Customers in 48 Hours" -> 跳到页底 #early-access

用户看到三个按钮，不确定区别是什么。

**问题 2：信任标记来源不明**

Hero 下方的 "4.9 / 5 . 53 early users" -- 这个评分来自哪里？没有链接到 G2、Product Hunt 或任何第三方平台。用户可能质疑真实性。

**问题 3：右侧 preview 卡片价值不清**

Hero 右侧有一个 "Free Preview" 轮播（5 slides：Who We Serve / Customer Cost / Competitors / Best Clients / Market Size），这是非常好的价值展示，但：
- 标题说 "Free Preview" 却没有明确 CTA 引导用户获取自己的版本
- 底部的 "Get your full report" 链接指向失效的 /report
- 轮播内容是固定的 Therapy 行业数据，来访的 freelancer 或 pest control 老板看到可能觉得不相关

### 2.3 Hero 区改进建议

```
建议主 CTA：统一为一个——"See Your Free Market Snapshot"
指向：/report（修复路由后）
次 CTA：移除导航栏 "Get More Revenue"，保留 "Get started" 改为 "Sign in"
```

**建议 headline 备选**（A/B 测试）：

| 方案 | Headline | 理由 |
|------|----------|------|
| A（当前） | Your AI growth team. Done for you. | 感性，但 "growth team" 不够具体 |
| B | Get new customers in 48 hours. No agency. No DIY. | 直击结果 + 消除两大替代方案 |
| C | The $49 marketing team for one-person businesses. | 价格锚点 + 精准受众 |

---

## 3. 定价区诊断

### 3.1 价格一致性问题（严重）

页面上至少出现 **4 套不同的价格表述**，互相矛盾：

| 位置 | 表述 | 价格 |
|------|------|------|
| Hero 区 | "Starting at $49" | $49 |
| 定价卡 Strategy | "$4.99 one-time" | $4.99 |
| 定价卡 Launch | "$49 token-based" | $49 |
| How It Works Step 1 | "Tell us your goal -- from $49" | $49 |
| How It Works Step 2 | "We build your full marketing stack -- $200" | $200 |
| FAQ | "What exactly does Auxora build for $200?" | $200 |
| Footer | "From $49" | $49 |

**用户困惑点**：

- Hero 说 "Starting at $49"，但定价卡里有 $4.99 选项，那到底从多少开始？
- How It Works Step 1 说 "$49"，Step 2 说 "$200" -- 是额外收费还是总价？
- FAQ 问 "$200" 但定价卡只标 $49 -- 这是同一个产品吗？
- "token-based" 是什么意思？从未解释

### 3.2 定价卡结构分析

| 层级 | 价格 | CTA | CTA 指向 | 问题 |
|------|------|-----|---------|------|
| Free | $0 | "Get my free snapshot" | /report | **路由失效** |
| Strategy | $4.99 | "Get my strategy report" | /report | **路由失效** |
| Launch | $49 (Most popular) | "Get new customers in 48 hours" | #early-access | 跳到邮件表单而不是购买流程 |

**三张卡的 CTA 分别指向两个不同位置**，其中两个还是失效的。"Most popular" 的 $49 卡片 CTA 不是购买按钮，而是一个邮件收集表单。用户期待点击后进入支付/开始流程，结果被带到页底填邮箱，期望落差巨大。

### 3.3 定价改进建议

**立即修复**：
1. 统一价格叙事：明确 Free -> $4.99 -> $49 是三个递进的产品层级，不是同一个东西的不同说法
2. How It Works 的 "$200" 改为 "$49"（或如果确实是 $200，在定价卡上标清楚 $49 是起步价/$200 是完整服务）
3. 所有 CTA 指向实际可用的页面：Free/Strategy 去 /report（修复后），Launch 去 /signup 或购买页

**结构建议**：

```
Free ($0)          -> 即时生成，不需登录 -> /report?plan=free
Strategy ($4.99)   -> 生成后支付解锁     -> /report?plan=strategy
Launch ($49)       -> 注册 + 支付 + 48hr 交付 -> /signup?plan=launch
```

---

## 4. 信任与社会证明诊断

### 4.1 当前信任元素

| 元素 | 位置 | 评价 |
|------|------|------|
| "4.9/5 . 53 early users" | Hero 下方 | 无来源链接，可信度低 |
| 滚动 marquee 条 | Hero 下方 | 6 条一句话成果，但无链接到详情 |
| 数据板：10x / 3x / 62% / 6 wks | Results 区 | 数字有冲击力，但缺少对应案例链接 |
| 4 条客户证言 | Results 区 | 有名字、职业、行业，质量中等 |
| 视频按钮 | Results 区底部 | "Watch a real founder story" -- demo-poster.jpg 404，图片不显示 |

### 4.2 信任链断裂点

1. **证言缺乏可验证性**：Sarah K.、Marcus T.、Dr. Jamie R.、Alex W. -- 全部只有名字首字母+头衔，没有照片、没有公司链接、没有 LinkedIn。对一个新品牌，这种证言容易被认为是编造的
2. **视频缩略图 404**：`/static/demo-poster.jpg` 返回 404，founder story 视频区域显示为灰色空白，反而降低信任
3. **无第三方背书**：没有 "As seen on"、没有合作伙伴 logo、没有媒体提及
4. **copyright 写 2025**：当前是 2026 年，页脚 "© 2025 Auxora.ai" 暗示网站很久没更新

### 4.3 改进建议

- 修复 demo-poster.jpg 404（或移除视频区域）
- 证言加上真实头像（即使是AI生成的人物图也比纯色首字母圆圈好，但最好是真实用户）
- "4.9/5" 链接到 G2 或 Product Hunt 评价页（需要先注册这些平台）
- 更新 copyright 为 2026
- 加入 "As featured in" 区域（等有媒体曝光后）

---

## 5. 注册/登录页诊断

### 5.1 登录页

![登录页](https://raw.githubusercontent.com/calderbuild/AuxoraAI/main/docs/screenshots/auxora-login-page.png)

- 视觉质量高：深色左栏 + 浅色右栏双栏布局，有产品截图和 testimonial
- 左栏证言与首页 Sarah K. 相同但描述不同（登录页写 "Co-founder, B2B SaaS"，首页写 "Skincare founder, solo business"）-- **人设不一致，降低可信度**
- placeholder "you@company.com" 暗示企业用户，但 Auxora 定位是 solopreneur -- 应改为 "you@yourbusiness.com" 或 "jane@example.com"
- 无 "Forgot password?" 链接

### 5.2 注册页

![注册页](https://raw.githubusercontent.com/calderbuild/AuxoraAI/main/docs/screenshots/auxora-signup-page.png)

- 3 个字段（Name / Email / Password），摩擦度合理
- 左栏列出 "What you get"（4 项 checklist），转化说服元素到位
- 没有 Google/Apple OAuth -- 对 solopreneur 用户群来说，社交登录能显著降低注册门槛
- 无 Terms/Privacy 链接在表单旁（合规风险）
- "min. 8 characters" 密码要求清晰
- CTA "Create my account" 文案清晰

### 5.3 注册流改进建议

| 优先级 | 改进 |
|--------|------|
| P0 | 统一 Sarah K. 的人设描述 |
| P0 | 添加 "Forgot password?" 到登录页 |
| P1 | 加 Google OAuth 一键注册 |
| P1 | 注册按钮旁添加 Terms/Privacy 链接 |
| P2 | 考虑无需注册即可体验 Free tier -- 直接在 /report 填业务信息就生成报告，生成后再要求注册查看完整版 |

---

## 6. 移动端诊断

![移动端 Hero 区（390px）](https://raw.githubusercontent.com/calderbuild/AuxoraAI/main/docs/screenshots/auxora-mobile-hero.png)

![移动端定价区（390px）](https://raw.githubusercontent.com/calderbuild/AuxoraAI/main/docs/screenshots/auxora-mobile-pricing.png)

### 6.1 整体评价

移动端适配质量较好，主要内容均正常显示。但存在以下问题：

| 问题 | 严重程度 | 说明 |
|------|---------|------|
| 导航栏两个按钮挤在一起 | 中 | "Get More Revenue" 和 "Get started" 在 390px 宽度下按钮文字被截断为三行，视觉混乱 |
| Hero 区上方大面积空白 | 中 | subheadline 和 H1 之间有大段空白（约 100px），浪费首屏黄金空间 |
| Agency vs Auxora 对比表 | 低 | 竖向堆叠后需要大量滚动，但结构仍清晰 |
| 定价卡横向排列 | 低 | 三张卡需要横向滚动或堆叠，Free 卡可能在首屏外 |

### 6.2 移动端改进建议

- 导航栏在移动端只保留一个主 CTA + 汉堡菜单
- 移除 Hero 上方空白或缩小间距
- 定价卡在移动端默认展开 "Most popular"（$49），其他折叠

---

## 7. 内容与文案诊断

### 7.1 优势

- **Pain point 区域写得极好**："Meta & Google ads feel like a black box"、"DIY marketing eats your whole week" -- 精准命中 solopreneur 痛点
- **Agency vs Auxora 对比表**：视觉清晰、数据对比有力（30 days vs 48 hrs, $2000+ vs $49）
- **垂直行业分区**：6 个行业各有独立文案，证明产品不是 generic 工具
- **FAQ 问题选择合理**：覆盖了最常见的购买异议

### 7.2 问题

| 问题 | 位置 | 说明 |
|------|------|------|
| 页面过长 | 整体 | 首页从头到尾超过 10 屏，信息过载 |
| "28 million" 重复 3 次 | Hero、Features、Who It's For | 同一个数据点在三个不同 section 重复出现，降低冲击力 |
| 行业 SEO 关键词外露 | Who It's For 区 | 每个行业卡片下面直接裸写 "therapist private practice marketing . how to get therapy clients online" -- 这是 SEO 关键词，不应该直接暴露给用户看 |
| Tesla 类比可能反感 | How It Works 区 | "Like setting up Tesla auto-drive" -- Tesla 的自动驾驶争议不少，对 non-tech solopreneur 来说不一定是积极类比 |
| "from $49" vs "from $4.99" | 多处 | 前面分析过的价格混乱 |

### 7.3 文案改进建议

- 缩短首页：将 "Who It's For" 6 个行业合并为 3-4 个 tab 或只展示最相关的 3 个
- "28 million" 只在一个地方出现
- 移除行业卡片中裸露的 SEO 关键词（或改为正文自然融入）
- Tesla 类比可替换为更中性的比喻："Like hiring a marketing team that works while you sleep"

---

## 8. 页面缺失项

| 缺失 | 影响 | 优先级 |
|------|------|--------|
| /report 页面不工作 | 免费获客入口完全断裂 | P0 |
| 无独立垂直行业页 | /for/therapists 等独立页面可以承接搜索流量 | P2 |
| 无 About / Team 页 | 新品牌缺乏信任基础 | P2 |
| 无 Blog / Resources | 无内容营销入口 | P2 |
| 无 Demo / Product Tour 页 | 用户无法在注册前看到产品界面 | P1 |
| 无 404 页面 | 失效链接显示空白 | P1 |

---

## 9. 修复优先级路线图

### P0 -- 本周必须修（转化链断裂）

| # | 任务 | 原因 |
|---|------|------|
| 1 | **修复 /report 路由** | 首页 5 个 CTA 指向 /report，全部失效。这是当前最大的转化漏洞 |
| 2 | **修复 /static/demo-poster.jpg 404** | Results 区视频缩略图空白，反而降低信任 |
| 3 | **统一价格表述** | $49 / $200 / $4.99 在页面上互相矛盾，用户不知道实际要付多少钱 |
| 4 | **修复 favicon 404** | 浏览器标签页无图标，不专业 |
| 5 | **更新 copyright 为 2026** | "© 2025" 暗示网站过时 |

### P1 -- Launch 前必须做（两周内）

| # | 任务 | 原因 |
|---|------|------|
| 6 | **统一 CTA 层级**：一个主 CTA（"See Your Free Market Snapshot" -> /report），一个次 CTA（"Sign in" -> /login） | 消除用户选择困难 |
| 7 | **统一 Sarah K. 人设**（登录页 vs 首页描述不一致） | 被发现不一致会严重损害信任 |
| 8 | **添加 "Forgot password?"** | 登录页基本功能缺失 |
| 9 | **移除行业卡片裸露的 SEO 关键词** | 用户看到原始关键词会觉得不专业 |
| 10 | **移动端导航栏优化**：只保留一个 CTA + 汉堡菜单 | 当前两个按钮在小屏上文字截断 |
| 11 | **FAQ 默认 SSR 渲染** | 当前折叠态内容搜索引擎不可见（同时也是 AI SEO 问题） |

### P2 -- Launch 后持续迭代

| # | 任务 | 原因 |
|---|------|------|
| 12 | 加 Google OAuth 注册 | 降低注册摩擦 |
| 13 | "无需注册" 的 Free tier 体验 | 降低首次体验门槛 |
| 14 | 独立垂直行业页（/for/therapists 等） | 承接搜索流量 + 提高相关性 |
| 15 | About / Team 页面 | 增加品牌信任 |
| 16 | 产品 Demo / Tour 页面 | 让用户注册前看到产品界面 |
| 17 | 首页长度优化（缩短 30%） | 当前 10+ 屏过长，信息重复 |

---

## 10. A/B 测试建议

Launch 后有一定流量时，建议按此顺序测试：

| 测试 | 假设 | 指标 |
|------|------|------|
| Hero headline：当前 vs "Get new customers in 48 hours" vs "The $49 marketing team" | 结果导向 headline 比品牌导向 headline 转化更高 | CTA click rate |
| 主 CTA：邮件收集 vs 直接跳 /report | 减少一步摩擦会提高转化 | Signup rate |
| 定价卡顺序：Free 居中 vs Launch 居中 | 推荐层级前置会提升付费转化 | Plan selection |
| 首页长度：当前 vs 精简版（移除重复段落） | 更短的页面减少流失 | Scroll depth + CTA rate |
| 移除 "4.9/5 . 53 early users"（无第三方来源） | 不可验证的评分可能反而降低信任 | Signup rate |

---

## 11. Staging vs Production 对比（staging.auxora.ai vs app.auxora.ai）

### 结论：首页完全相同，所有 CRO 问题两边都有

| 维度 | staging.auxora.ai | app.auxora.ai（即将 launch） |
|------|------------------|---------------------------|
| 首页内容 | 完全一致 | 完全一致 |
| /report 路由 | 失效（回退首页） | 失效（回退首页） |
| /dashboard | 可访问（有测试账号登录态） | 重定向到 /login |
| favicon | 404 | 404 |
| demo-poster.jpg | 404 | 404 |
| copyright | 2025（过时） | 2025（过时） |

### Staging Dashboard 额外发现

![Staging Dashboard](https://raw.githubusercontent.com/calderbuild/AuxoraAI/main/docs/screenshots/staging-dashboard.png)

Staging 有登录态，可以看到产品内部。Dashboard 显示 4 个测试项目：
- Karen Lum Consulting（klumconsulting.com）
- Local Pest Solutions（localpestsol.com）
- Here Counseling（herecounseling.com）
- Auxora（app.auxora.ai）

#### 产品内部结构（以 Here Counseling 为例）

产品采用**左侧聊天 + 右侧画布**的双栏布局：

**左侧 -- AI 对话面板**：
- Auxora AI 引导用户完成 3 问快速访谈（业务描述、当前阶段、90 天目标）
- 访谈完成后触发 Report Preview -> Full Report 生成
- 后续可通过对话触发 "Launch ads"、"Build landing page" 等动作
- 底部有建议操作按钮（Launch Meta Campaign / Set Up Analytics / Build Landing Pages）

**右侧 -- 内容画布（Pipeline）**：
- 顶部 Pipeline 导航：Interview -> Research -> GTM Report -> Product Manager -> Landing Page -> Campaigns
- 底部 Tab 导航：Dashboard / Media Library / Campaigns / Brand DNA
- Brand DNA 页面展示从用户网站自动提取的品牌信息（logo、配色、字体、tagline、target audience、value proposition 等）

#### 产品内页 CRO 观察

| 发现 | 严重程度 | 说明 |
|------|---------|------|
| 产品内页质量高 | 正面 | Brand DNA 自动提取、对话式引导、Pipeline 可视化都做得好 |
| 首页完全没有展示产品 UI | 高 | "How it works" 区域有一个标注 "app.auxora.ai/workspace" 和 "LIVE" 的产品截图区域，但图片未渲染（demo 区域空白），用户无法在注册前看到产品界面 |
| 对话面板无 empty state 引导 | 中 | 新项目创建后，第一条消息是 AI 要求提供 URL -- 如果用户没有网站，不确定该怎么做（虽然文案提到了 "No website? Just describe your business"） |
| Pipeline 状态不可见于首页 | 中 | 首页 "How it works" 4 步流程和产品内的 6 步 Pipeline（Interview -> Research -> GTM Report -> Product Manager -> Landing Page -> Campaigns）不一致。首页说 4 步，产品实际是 6 步 |

#### Launch 前产品体验建议

| 优先级 | 建议 |
|--------|------|
| P0 | 首页 "How it works" demo 区域修复：要么放一段产品录屏/GIF，要么放 Brand DNA 页面的真实截图。当前空白区域是转化杀手 |
| P1 | 首页流程描述（4 步）和产品 Pipeline（6 步）对齐，否则用户进入产品后会困惑 |
| P1 | /report 路由修复 -- 让未登录用户也能输入业务信息并看到 Free tier preview（最关键的获客入口） |
| P2 | 产品 Demo Tour：在首页或独立页面放一个 3-5 张截图的产品 walkthrough |

---

## 附录 A：术语表

本报告涉及的关键术语解释，按出现顺序排列：

| 术语 | 含义 |
|------|------|
| **CRO** | Conversion Rate Optimization（转化率优化）。研究怎么让更多访客完成你想要的动作（注册、付费等） |
| **转化** | 用户完成了你设定的目标动作。填邮箱 = 一次转化，注册 = 一次转化，付费 = 一次转化 |
| **转化率** | 完成目标动作的人数 / 总访客数。100 人来了 5 人注册 = 5% 转化率 |
| **CTA** | Call to Action（行动号召），就是页面上引导用户做某事的按钮。"Get started"、"Get my free report" 都是 CTA |
| **Hero 区** | 页面最顶部、不滚动就能看到的区域。是最值钱的位置，100% 的访客都会看到 |
| **转化漏斗** | 用户从"看到你"到"付钱"的完整路径。每一步都会漏掉一些人，形状像漏斗 |
| **Social Proof** | 社会证明 -- 让新访客相信你靠谱的元素：客户评价、评分、用户数、知名客户 logo 等 |
| **A/B 测试** | 同时运行两个版本的页面，随机给不同用户看，比较哪个版本转化率更高 |
| **SPA** | Single Page Application（单页应用）。浏览器下载空壳 HTML 后用 JavaScript 渲染内容。人能看到，但搜索引擎爬虫可能看到空白 |
| **SSR** | Server-Side Rendering（服务端渲染）。服务器先生成完整内容再发给浏览器，人和爬虫都能看到 |
| **OAuth** | "用 Google/Apple 账号一键登录"的技术协议。用户不需要记新密码 |
| **ROAS** | Return on Ad Spend（广告支出回报率）。花 $1 广告费赚回 $2 = ROAS 2x |
| **CAC** | Customer Acquisition Cost（获客成本）。获得一个新客户平均要花多少钱 |
| **ICP** | Ideal Customer Profile（理想客户画像）。你最好的客户长什么样 |
| **Pipeline** | 产品内的工作流阶段，类似"流水线"。Auxora 的 Pipeline 是：Interview -> Research -> Report -> Product Manager -> Landing Page -> Campaigns |

---

## 附录 B：诊断方法

| 维度 | 工具 |
|------|------|
| 首页完整内容 | Playwright browser_snapshot（accessibility tree） |
| 视觉检查 | Playwright browser_take_screenshot（桌面 1280px + 移动端 390px） |
| 路由测试 | Playwright browser_navigate 测试 /report、/dashboard、/login |
| 注册流测试 | Playwright 点击 "Create one free" 检查注册表单 |
| 产品内页 | Playwright 在 staging 已登录态下检查 dashboard 和 project 内页 |
| Console 报错 | Playwright console 日志（favicon 404, demo-poster 404, auth 401） |
| 双环境对比 | 分别对 staging.auxora.ai 和 app.auxora.ai 执行同一套检查 |
