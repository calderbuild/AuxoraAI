---
title: Auxora.ai 注册流程转化率诊断报告
type: report
date: 2026-03-27
author: Calder
audience: Hui Li (CEO)
---

# Auxora.ai 注册流程转化率诊断报告

## 诊断结论

注册表单本身摩擦度合理（3 个字段），但**围绕表单的信任链和体验细节存在多处断裂**：无 OAuth、无 Terms 链接、无密码找回、浏览器原生验证替代了自定义错误提示、移动端社会证明完全消失、testimonial 人设跨页面不一致。这些问题单独影响不大，叠加后会造成可感知的"半成品"印象，对一个定价 $200/月的产品尤其致命。

---

## 1. 注册流程结构

当前流程为**登录/注册同页切换**，URL 始终为 `/login`，通过按钮在两种表单状态间切换。

| 维度 | 登录态 | 注册态 |
|------|--------|--------|
| 标题 | Sign in | Create account |
| 字段 | Email + Password（2 个） | Name + Email + Password（3 个） |
| CTA | Sign in -> | Create my account -> |
| 左栏 | Sarah K. testimonial + 统计数据 | "What you get" checklist + 统计数据 |
| 切换入口 | "No account yet? Create one free ->" | "Already have one? Sign in ->" |

**正面**：3 字段注册是 SaaS 最佳实践，摩擦度低。左栏注册态展示 4 条价值承诺（competitor analysis / GTM roadmap / customer segments / live AI research），说服力到位。

---

## 2. 逐项摩擦点诊断

### 2.1 Testimonial 人设不一致（严重）

登录页左栏 Sarah K. 标注 "Co-founder, B2B SaaS"，首页同一人物标注 "Skincare founder, solo business"。两个完全不同的行业和角色。被用户发现后信任归零 -- 一个连 testimonial 都编不圆的产品，凭什么收 $200/月？

**修复**：统一为一个人设，优先与目标客群一致（solopreneur，非 B2B SaaS co-founder）。

### 2.2 Email placeholder 错位

`you@company.com` 暗示企业用户，与 "Built for one-person businesses" 定位矛盾。Solopreneur 用的是 `jane@gmail.com` 或 `jane@janestherapy.com`，不是 `you@company.com`。

**修复**：改为 `you@yourbusiness.com` 或 `jane@example.com`。

### 2.3 无 Google OAuth

Solopreneur 群体（therapists、pest control、freelancers）大概率用 Gmail 作为主力邮箱。Google OAuth 一键注册可以将注册摩擦从"填 3 个字段 + 想密码"降到"点一下"。行业基准显示社交登录可提升注册转化 20-50%。

**修复**：至少加 Google OAuth，放在表单上方，用分隔线 "or" 与邮箱表单分开。

### 2.4 无 Forgot Password

登录页完全没有密码找回入口。用户忘记密码后唯一选择是放弃。这是基础功能缺失。

**修复**：Password 字段下方加 "Forgot password?" 链接。

### 2.5 无 Terms / Privacy 链接

注册按钮旁无任何法律文本。在美国市场，CCPA 要求在收集个人信息前告知隐私政策。合规风险之外，"By signing up, you agree to our Terms and Privacy Policy" 本身也是信任信号 -- 它暗示"我们是正规公司"。

**修复**：CTA 按钮下方加一行小字 "By creating an account, you agree to our [Terms] and [Privacy Policy]"。

### 2.6 浏览器原生验证

当前表单提交空字段或格式错误时，弹出的是浏览器默认气泡（中文系统显示中文提示），视觉粗糙且不可控。无内联实时验证，无自定义错误样式。

**修复**：
- 添加 inline validation（失焦时校验）
- 自定义错误消息，与品牌视觉一致
- Password 字段加实时强度指示器
- Email 字段加常见拼写纠错（gmial.com -> gmail.com）

### 2.7 无密码显示切换

Password 字段没有 show/hide toggle（眼睛图标）。用户在注册时设定新密码，看不到自己输了什么会增加焦虑。

**修复**：加 eye icon toggle，默认隐藏，点击显示。

### 2.8 Input 缺少 name 属性

三个 input 都没有 `name` 属性（`id` 有但 `name` 为空），这会影响部分浏览器和密码管理器的自动填充行为。`autocomplete` 属性设置正确（`name` / `email` / `new-password`），部分弥补了这个问题。

**修复**：给每个 input 加 `name` 属性（`name="name"` / `name="email"` / `name="password"`）。

---

## 3. 移动端诊断（390x844）

| 问题 | 影响 |
|------|------|
| 左栏完全隐藏 | 注册态的 "What you get" checklist 在移动端不可见，用户只看到一个光秃秃的表单，没有任何价值承诺或社会证明 |
| 无 sticky CTA | 表单虽短不需要 sticky，但如果未来加字段要注意 |
| 键盘弹出后表单位置 | 实际设备上需验证键盘弹出后 CTA 按钮是否被遮挡 |

**核心问题**：移动端注册页失去了所有说服元素。一个首次访客在手机上看到的只是 "Create account" 标题 + 3 个空白输入框 + 一个按钮。没有任何理由告诉他为什么要注册。

**修复**：在移动端表单上方插入精简版价值承诺（1-2 行文案 + 统计数据），不需要复制整个左栏。

---

## 4. 改进建议

### Quick Wins（1-2 天，无需工程架构变更）

| # | 改进 | 预期影响 |
|---|------|---------|
| 1 | 统一 Sarah K. 人设（登录页 vs 首页） | 消除信任破坏 |
| 2 | Email placeholder 改为 `you@yourbusiness.com` | 与 solopreneur 定位对齐 |
| 3 | CTA 下方加 Terms / Privacy 链接 | 合规 + 信任信号 |
| 4 | 登录页加 "Forgot password?" | 基础功能补全 |
| 5 | Password 字段加 show/hide toggle | 减少新密码设置焦虑 |
| 6 | Input 加 `name` 属性 | 改善自动填充兼容性 |

### High Impact（1-2 周，需要工程支持）

| # | 改进 | 预期影响 |
|---|------|---------|
| 7 | 加 Google OAuth | 注册转化提升 20-50% |
| 8 | 自定义 inline validation 替换浏览器原生 | 体验专业度提升 |
| 9 | 移动端表单上方加精简版价值承诺 | 移动端注册转化提升 |
| 10 | Email 常见拼写纠错（did you mean gmail.com?） | 减少无效注册 |

### Test Ideas（有流量后 A/B 测试）

| 假设 | 测试方案 | 指标 |
|------|---------|------|
| 减少字段能提升转化 | 移除 Name 字段（注册后再收集） | 注册完成率 |
| OAuth 优先展示更高效 | Google OAuth 在上 vs 邮箱表单在上 | 注册完成率 |
| CTA 文案影响点击意愿 | "Create my account" vs "Start free" vs "Get my strategy" | CTA 点击率 |
| 注册前体验产品更高效 | 先填业务 URL 看 preview -> 再要求注册 | 注册转化率 |

---

## 5. CTA 文案替代方案

| 位置 | 当前文案 | 建议替代 | 理由 |
|------|---------|---------|------|
| 注册 CTA | Create my account -> | Get my free strategy -> | 强调注册后立即获得的价值 |
| 切换到注册 | Create one free -> | Start free -> | 更简洁 |
| 注册页副标题 | Create your free account and get your personalized GTM strategy in under 10 minutes. | See your competitors, customers, and growth plan -- free, in 10 minutes. | 具体化价值而非描述动作 |
| 切换到登录 | Already have one? Sign in -> | （保持不变） | 当前文案已足够清晰 |

---

## 6. 诊断方法

| 维度 | 工具 |
|------|------|
| 页面结构 | Playwright `browser_snapshot` 获取 accessibility tree |
| 视觉检查 | Playwright `browser_take_screenshot`（桌面 1440px + 移动 390x844） |
| 表单验证 | Playwright `browser_run_code` 提交空表单 / 无效数据，检查 validation 行为 |
| 元素属性 | Playwright `evaluate` 检查 input type / required / autocomplete / name / minLength |
| 信任元素 | 检查 OAuth / Terms / Privacy / Forgot Password / password toggle 是否存在 |

截图存档：`staging-login.png`、`staging-signup.png`、`staging-signup-mobile.png`（项目根目录）。
