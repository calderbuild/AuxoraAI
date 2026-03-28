---
title: Auxora.ai 4/1 发布策略报告
type: report
date: 2026-03-27
author: Calder
audience: Hui Li (CEO)
---

# Auxora.ai 4/1 发布策略报告

## 核心判断

距 launch 还有 5 天。当前最大风险不是曝光不足，而是**流量进来后转化链断裂**。/report 路由失效意味着所有导流终点都是死链接。建议：先修管道，再开水龙头。

---

## 一、Launch 前阻断项（3/28-3/31 必须完成）

### P0 技术阻断（工程团队）

| 项目 | 原因 | 负责人建议 |
|------|------|-----------|
| 修复 /report 路由 | 首页 5 个 CTA 指向此处，全部回退首页。免费获客入口断裂 | Tingyong/Yuhong |
| 解除 robots.txt AI 爬虫封杀 | GPTBot、ClaudeBot、Google-Extended 全被 Disallow，AI 搜索可见度为零 | Tingyong |
| 修复 demo-poster.jpg 404 | Results 区域视频缩略图空白，削弱信任感 | Yuhong |
| 统一价格表述 | $49/$200/$4.99 三套价格同时出现，用户困惑 | Hui Li 定方案，工程执行 |
| 接入 GA4 基础事件 | 无追踪 = 无法衡量 launch 效果。最小集：`page_view`、`sign_up`、`generate_lead` | Tingyong |

### P1 内容准备（Calder）

| 项目 | 截止 |
|------|------|
| 撰写 3 个垂直行业的 Reddit 评论草稿（therapist/pest control/consultant） | 3/29 |
| 准备 Product Hunt launch 文案（tagline + description + 3 张截图） | 3/30 |
| 检查 staging 与 production 一致性，确认修复已同步 | 3/31 |

---

## 二、发布执行计划

### D-Day：4/1（周二）

- 工程团队确认所有 P0 修复已部署到 production
- Calder 做最终 smoke test：/report 路由、价格一致性、demo 图片、GA4 事件触发
- 内部 Slack 通知：launch 状态 green/red
- **不在 4/1 当天做任何外部推广**。用这一天做最后验证

### Week 1 逐天计划（4/2-4/6）

| 日期 | 动作 | 产出 |
|------|------|------|
| 4/2 (三) | Reddit 养号：在 r/therapists、r/pestcontrol 各发 1 条真诚价值帖（不提产品） | 2 条帖子 |
| 4/3 (四) | Reddit 继续养号：在 r/freelance、r/smallbusiness 回复 2-3 个热帖 | 3 条评论 |
| 4/4 (五) | 在 r/SaaS 或 r/EntrepreneurRideAlong 发第一个 "build in public" 帖 | 1 条帖子 |
| 4/5 (六) | 整理第一周 GA4 数据，写周报 | 数据快照 |
| 4/6 (日) | 准备下周 Product Hunt 提交材料 | PH 草稿 |

### Week 2（4/7-4/13）

- Product Hunt launch（建议周二 4/8，避开周一竞争）
- Reddit 发布第一条 "Show HN" 风格的产品帖（r/SaaS）
- 开始 3 篇对比内容：Auxora vs Jasper / vs GoHighLevel / vs DIY marketing
- 在 G2、Capterra 创建产品页面

---

## 三、Reddit 策略

### 账号现状

u/BeatImpress___ 接近零 karma，直接发产品帖会被 automod 拦截或被社区当 spam。必须先养号。

### 养号策略（4/1-4/7，至少积累 50+ comment karma）

1. **选 3-4 个目标 subreddit 潜水**：r/therapists (95K)、r/pestcontrol (12K)、r/freelance (300K)、r/smallbusiness (900K)
2. **每天回复 2-3 个帖子**，提供真实有用的建议（marketing tips、客户获取经验），不提 Auxora
3. **避免**：新账号一上来就发链接、跨多个 sub 发同样内容、评论里加 CTA

### 正式推广节奏（4/8 起）

- **帖子类型**：build-in-public 故事（"我们怎么帮一个 therapist 3 天内搞定 marketing plan"），不要硬广
- **频率**：每周 2-3 条评论 + 1 条原创帖
- **核心 sub**：r/SaaS、r/EntrepreneurRideAlong、r/startups（发产品帖）；垂直 sub 只回复不发帖

---

## 四、Product Hunt Launch 建议

- **时间**：4/8（周二），Pacific Time 00:01 上线
- **前置**：提前一周在 PH 创建 Coming Soon 页面，邀请现有 7 个客户关注
- **Tagline 方向**："Your entire marketing team, powered by AI. $49, done in 48 hours."
- **关键素材**：3 张产品截图（Pipeline 可视化、Brand DNA 提取、GTM Report 示例）、1 个 60s demo GIF
- **Hunter**：如果团队没有高 karma PH 账号，找一个 PH 活跃用户 hunt。Hui Li 的 MiraclePlus/YC 网络可以帮忙
- **风险**：PH 社区对 AI wrapper 审美疲劳，必须强调 "done-for-you" 差异化而非 "another AI tool"

---

## 五、成功指标

### 第一周 KPI（4/1-4/7）

| 指标 | 目标 |
|------|------|
| /report 页面访问量 | > 100 UV |
| 免费 Snapshot 生成数 | > 20 |
| $4.99 Report 购买 | > 5 |
| Reddit comment karma 增长 | > 50 |
| GA4 事件正常触发 | 100% |

### 第一月 KPI（4 月）

| 指标 | 目标 |
|------|------|
| 新注册用户 | > 100 |
| 付费用户（$4.99+$49） | > 15 |
| MRR | $10K -> $12K |
| Product Hunt upvotes | > 100 |
| 第三方平台存在 | PH + G2 + 至少 2 个 Reddit 帖子 |

---

## 六、风险与 Contingency

| 风险 | 概率 | 应对 |
|------|------|------|
| P0 技术问题 4/1 前未修完 | 中 | 推迟外部推广到修复后，不推迟内部 launch 日期 |
| Reddit 账号被 shadowban | 低 | 准备备用账号；降低发帖频率 |
| Product Hunt 反响冷淡（< 50 upvotes） | 中 | 不依赖 PH 做唯一渠道；同步推进 Reddit + 对比内容 |
| 免费 Snapshot 转付费率 < 5% | 高 | 复盘 /report 到 /login 的转化漏斗，优化 CTA 文案 |
| dogfooding 发现的 bug（URL 丢失、Profile 退化）影响付费体验 | 高 | 优先修复 URL 丢失 bug；准备人工补救流程 |

---

## 下一步

1. **今天（3/27）**：将 P0 阻断项清单同步给 Tingyong/Yuhong，确认 3/31 前能否全部修复
2. **3/28**：开始 Reddit 养号（第一条评论）
3. **3/29**：完成 Product Hunt Coming Soon 页面
4. **3/31**：全量 smoke test，go/no-go 决策
