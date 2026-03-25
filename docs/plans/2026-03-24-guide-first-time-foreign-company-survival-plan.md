---
title: 第一次进外企生存指南 -- 工具、文化、实操全梳理
type: guide
date: 2026-03-24
context: Calder 加入 Auxora.ai（美国初创，5-10 人分布式团队），GTM 工程师实习
---

# 第一次进外企生存指南

> 面向中国人首次加入美国科技初创公司的全面准备清单。
> 基于 Auxora.ai 的实际情况（5-10 人分布式团队，async-first，Daily Standup）定制。

---

## 一、常用软件工具全景

### 1.1 日常沟通

| 工具 | 用途 | 优先级 | 中国访问 |
|------|------|--------|----------|
| **Slack** | 团队异步消息主力，频道化沟通 | 必装 | 需代理 |
| **Zoom** | 视频会议（Daily Standup、1:1） | 必装 | 需代理（偶尔可直连但不稳） |
| **Google Meet** | Google Workspace 用户自带的视频方案 | 备选 | 需代理 |
| **Loom** | 异步视频录制，跨时区讲解用 | 推荐 | 需代理 |

### 1.2 项目管理

| 工具 | 说明 | 适用场景 |
|------|------|---------|
| **Linear** | 2024-2026 初创最火项目管理，极简、键盘驱动 | 工程任务 |
| **Notion** | 万能工具：文档 + Wiki + 项目管理 + 数据库 | 全团队协作 |
| **Jira** | 老牌但重，大外企主流，小团队越来越少用 | 大型团队 |
| **Trello** | 看板式，极简 | 轻量追踪 |

### 1.3 文档协作

| 工具 | 说明 |
|------|------|
| **Google Workspace** | Gmail + Docs + Sheets + Slides + Drive + Calendar，美国初创标配 |
| **Notion** | 内部 Wiki、产品文档、会议纪要 |
| **Confluence** | Atlassian 生态，配合 Jira，偏大公司 |

### 1.4 代码与工程

| 工具 | 说明 |
|------|------|
| **GitHub** | 代码托管 + PR Review + CI/CD（GitHub Actions），绝对主流 |
| **VS Code / Cursor** | 编辑器。Cursor 是 2024-2025 爆发的 AI-native 编辑器 |
| **Claude Code** | CLI 编程助手 |
| **Sentry** | 错误监控，几乎每个团队都用 |

### 1.5 设计

| 工具 | 说明 |
|------|------|
| **Figma** | UI/UX 设计标准，实时协作 |
| **Canva** | 非设计师做营销素材、社交媒体图片 |
| **Excalidraw** | 手绘风格白板，技术架构图 |

### 1.6 云与部署

| 工具 | 说明 |
|------|------|
| **Vercel** | 前端部署零配置，Next.js 团队出品 |
| **Railway** | 后端一键部署，开发体验好 |
| **AWS** | 最全面云平台（中国有独立版本） |
| **Cloudflare** | CDN + DNS + Workers，性价比极高 |
| **Supabase** | Firebase 开源替代，PostgreSQL + Auth |

### 1.7 CRM / 分析 / AI

| 类别 | 推荐工具 |
|------|---------|
| CRM | **HubSpot**（初创首选，免费起步）、Apollo.io（B2B 情报） |
| 分析 | **GA4**（流量）、PostHog（产品分析，开源） |
| AI | **Claude / ChatGPT**（通用）、Cursor（编程）、Granola（会议纪要） |

### 1.8 HR / 财务

| 工具 | 说明 |
|------|------|
| **Deel / Remote.com** | 国际远程团队薪资、合规雇佣 |
| **Gusto** | 美国本土员工 HR/薪资 |
| **Mercury** | 初创银行账户 |
| **Brex / Ramp** | 企业信用卡 + 费用管理 |

### 1.9 中国访问总结

**几乎所有美国 SaaS 都需要代理**。少数例外：

- 无需代理：VS Code、Docker（本地）、Cursor（本体）
- 可自建：PostHog、Metabase、GitLab
- 不稳定直连：GitHub（时好时坏）、Zoom（偶尔可用）

**结论：稳定的网络代理是外企远程工作的第一前提。**

---

## 二、职场文化差异

### 2.1 扁平化 vs 层级制

| 国内习惯 | 外企（尤其初创）现实 |
|----------|---------------------|
| 叫领导"X 总""X 哥" | 直接叫名字（Hui、Calder），叫 Sir/Mr. 会显得奇怪 |
| 等领导指示再动 | 被期望主动发现问题、提出方案，不等安排 |
| 有想法先私下跟领导说 | 直接在公开频道说，transparency 是默认值 |
| 不好意思反驳上级 | "Disagree and commit" -- 鼓励先表达不同意见，最终决定后全力执行 |

**关键心态转变**：你不是"下属"，你是 team member。Leader 期望你像合作伙伴一样工作，不是等待指令的执行者。

### 2.2 沟通风格

**直接表达，不绕弯子：**

| 不要这样说 | 应该这样说 |
|-----------|-----------|
| "这个可能不太好吧..." | "I think approach B is better because..." |
| "我觉得大概差不多" | "I'll have it done by Thursday EOD" |
| "没什么问题"（其实有） | "I have a concern about X" |
| 沉默（表示不同意） | "I see it differently -- here's why..." |

**"I don't know" 是完全可以接受的：**
- "I'm not sure, let me check and get back to you" -- 这比假装知道好 100 倍
- "I haven't done this before, could you point me to an example?" -- 正常且被鼓励

### 2.3 会议文化

- **会议要有 agenda**：没有 agenda 的会议 = 不该开的会议
- **准时开始准时结束**：迟到 5 分钟在美国文化里是不专业的表现
- **会后要有 action items**：谁做什么、deadline 是什么
- **"This could have been a Slack message"**：能异步解决的不开会
- **你被期望发言**：整场会议一声不吭 = 你没在参与。哪怕说 "That makes sense, I agree" 也比沉默好

### 2.4 反馈文化

**给反馈：**
- 直接但建设性：不是 "这不行"，而是 "I think we could improve X by doing Y"
- PR Review 时坦率指出问题是正常的，不是在针对你

**收反馈：**
- 不要把代码反馈当人身攻击 -- "This function is too complex" 说的是代码，不是你
- 回应方式："Good point, I'll refactor" 或 "I chose this approach because... what do you think?"
- 定期 1:1 时主动问："What can I do better?"

### 2.5 Work-Life Balance

- 美国初创确实工作强度大，但 **不等于加班文化**
- 强调 output 而非 hours -- 没人盯你几点上线，但 deliver 质量和速度被关注
- **PTO（Paid Time Off）是你的权利**，不要觉得请假不好意思
- **WFH（Work From Home）是默认状态**，不需要特别申请

---

## 三、商务英语速成

### 3.1 必知缩写

| 缩写 | 全称 | 含义 |
|------|------|------|
| EOD | End of Day | 今天下班前 |
| ETA | Estimated Time of Arrival | 预计完成时间 |
| LGTM | Looks Good To Me | 代码审查通过 |
| PTAL | Please Take A Look | 请看一下 |
| WFH | Work From Home | 在家办公 |
| OOO | Out of Office | 不在，请假 |
| PTO | Paid Time Off | 带薪休假 |
| TL;DR | Too Long; Didn't Read | 摘要 / 说重点 |
| ASAP | As Soon As Possible | 尽快 |
| FYI | For Your Information | 供参考 |
| IMO / IMHO | In My (Humble) Opinion | 我个人认为 |
| WIP | Work In Progress | 进行中 |
| AFAIK | As Far As I Know | 据我所知 |
| AFK | Away From Keyboard | 暂时离开 |
| SHIP IT | -- | 可以上线了 / 发布吧 |
| NIT | Nitpick | 代码审查中的小建议 |
| RFC | Request For Comments | 征求意见（方案讨论） |
| ACK | Acknowledge | 收到/确认 |
| BLOCKER | -- | 阻塞问题，必须先解决 |

### 3.2 Daily Standup 模板

```
Yesterday: Finished the SEO keyword research for therapist vertical
Today: Working on the Reddit content calendar, will share draft by EOD
Blockers: Need access to the HubSpot account -- @Hui could you invite me?
```

注意：
- 简洁，每项 1-2 句话
- 明确说 blocker，不要藏着 -- Auxora 文化就是 "Blockers surface immediately"
- 不需要说 "Good morning everyone"，直接进主题

### 3.3 常用句型

**请求帮助：**
- "Hey [name], do you have a minute to help me with X?"
- "I'm stuck on X. Could you point me in the right direction?"
- "Quick question: is there an existing pattern for X?"

**表达观点：**
- "I think we should... because..."
- "One concern I have is..."
- "Have we considered...?"

**表示不确定：**
- "I'm not sure about this -- let me look into it"
- "I need to dig deeper before I can give a solid answer"

**跟进进度：**
- "Quick update: I'm about 70% done with X, on track for Thursday"
- "Heads up: this is taking longer than expected because of Y"

### 3.4 常用 Tech 行话

| 短语 | 含义 |
|------|------|
| Low-hanging fruit | 容易做到的事 |
| Move the needle | 产生实质影响 |
| Double down | 加大投入 |
| Ship it | 发布上线 |
| Dogfood | 自己用自己的产品 |
| Unblock | 解除阻塞 |
| Bandwidth | 精力/时间余量（"I don't have bandwidth for this"） |
| On my radar | 我知道这事了 |
| Circle back | 稍后再讨论 |
| Deep dive | 深入研究 |
| Alignment | 达成共识 |
| Context switch | 切换任务 |
| Scope creep | 需求蔓延 |
| MVP | 最小可行产品 |
| North Star | 核心指标/目标 |

---

## 四、Slack 使用礼仪

### 4.1 基本规范

- **用 thread（回复线程）**：不要在主频道刷屏，回复相关消息时点 "Reply in thread"
- **不要滥用 @here / @channel**：@here 通知所有在线的人，@channel 通知所有人（包括勿扰模式）。除非紧急事项，不要用
- **善用 emoji reaction**：用 :eyes:（在看了）、:white_check_mark:（完成了）、:+1:（同意）回应，减少噪音
- **设置状态**：出去吃饭设 "Lunch, back at 1pm"，请假设 "OOO until Monday"
- **DM vs Channel**：团队相关的讨论放公开频道（透明度），个人事务或敏感话题用 DM

### 4.2 消息格式

```
// 好的消息
@Hui Quick update on the Reddit strategy:
- Identified 5 target subreddits for therapist niche
- Draft content calendar ready for review: [link]
- Need your input on tone -- professional vs casual?

// 不好的消息
hi
are you there?
can I ask something?
（不要分开发，直接把问题说完整）
```

### 4.3 时区意识

- 在你的 Slack profile 里设好时区（UTC+8）
- 给美国同事发消息时，不要期待即时回复 -- 他们可能在睡觉
- 用 **Schedule Send**（定时发送）：把消息安排在对方工作时间发出
- 紧急事项标注 "URGENT" 或打电话

---

## 五、远程工作最佳实践

### 5.1 时区管理

- 中国时间 UTC+8，美西 PST/PDT UTC-8/-7
- **时差 15-16 小时**
- 实际重叠窗口：你的晚上 9-12 点 = 美西早上 5-8 点（勉强）
- 你的早上 8-10 点 = 美西下午 4-6 点
- **策略**：白天异步工作，晚上留 1-2 小时同步窗口开会

### 5.2 Over-Communication 原则

远程工作中，**没人看到你在干嘛**。不主动沟通 = 消失了。

- 每天 Standup 写清楚进展
- 卡住了**立刻说**，不要自己闷头研究两天 -- Auxora 文化明确要求这一点
- 完成一个阶段性成果就分享（"Here's what I have so far, feedback welcome"）
- 预计会延期就提前说（"Heads up: X is taking longer, new ETA is..."）

### 5.3 视频会议

- **开不开摄像头**：看团队文化。1:1 建议开，大会可以不开。第一周建议多开，建立 face recognition
- **背景**：整洁或用虚拟背景，不需要很正式
- **网络卡了**：说 "Sorry, I'm having connection issues" 然后切到纯语音
- **会议纪要**：养成习惯会后在 Slack/Notion 贴一份 summary + action items

### 5.4 建立存在感

- **Documentation is visibility**：你写的文档、你发的 update、你做的 demo 就是你的"存在感"
- **主动 demo**：做出东西就录个 Loom 视频展示
- **参与讨论**：不要只当执行者，对产品方向、策略有想法就说
- **帮助别人**：看到同事卡住了，主动问能不能帮上忙

---

## 六、入职前准备清单

### 6.1 网络（第一优先级）

- [ ] 搞定代理方案（自建 + 机场备用），确保能稳定访问 Google/Slack/GitHub
  - 推荐协议：VLESS + Reality 或 Hysteria2
  - 客户端：macOS 用 Clash Verge Rev 或 Surge
  - 配置分流规则：国内直连，国外走代理
- [ ] 配置 Git SSH proxy（`~/.ssh/config` 加 ProxyCommand）
- [ ] 测试视频会议稳定性（选延迟低的节点：日本/香港）
- [ ] 准备备用方案：第二个机场、手机热点

### 6.2 账号注册

- [ ] Google Workspace 账号（公司会发邀请）
- [ ] Slack -- 公司邀请链接加入
- [ ] GitHub -- 加入 organization
- [ ] Notion -- 团队 workspace
- [ ] Linear / Jira -- 项目管理
- [ ] Figma -- 如果涉及设计
- [ ] HubSpot -- GTM 角色需要

### 6.3 Profile 设置

- [ ] 每个工具里设置专业头像（真人照片，不要卡通）
- [ ] 写清楚你的角色和时区
  - 示例 bio："GTM Engineer Intern | UTC+8 (Beijing) | SEO, Reddit, Content"
- [ ] Slack 状态默认设置工作时间

### 6.4 收款

- [ ] 注册 **Wise** 账户，用护照验证身份
- [ ] 开通 USD 收款账户，获取美国银行账号 + routing number
- [ ] 把收款信息给公司（或在 Deel 平台填写）
- [ ] 了解个人年度结汇限额（5 万美元）
- [ ] 备选：注册 Payoneer 作为 backup

### 6.5 税务与法律

- [ ] 明确雇佣形式：Contractor 还是通过 EOR（Deel/Remote.com）
- [ ] 如果是 Contractor：保留合同原件、每月 invoice 记录
- [ ] 咨询一次懂跨境收入的会计/税务师（几百到几千元，必要投资）
- [ ] 了解个人所得税申报义务（中国税务居民全球收入需申报）
- [ ] 社保：以灵活就业人员身份缴纳养老 + 医保，或购买商业医疗保险

### 6.6 硬件与环境

- [ ] Mac 系统语言设英文（报错信息更容易搜索）
- [ ] 安装开发工具：Cursor/VS Code、iTerm2/Warp、Homebrew
- [ ] 配置 Git SSH + proxy
- [ ] 浏览器装 SwitchyOmega 或用系统代理
- [ ] 菜单栏加世界时钟，同时显示北京和美西时间
- [ ] 买一副好耳机（降噪，视频会议用）
- [ ] 确保网络带宽够用（推荐 100Mbps+）

---

## 七、常见踩坑与避坑

### 7.1 沟通踩坑

| 踩坑行为 | 正确做法 |
|----------|---------|
| 会议上全程沉默 | 哪怕说 "I agree" 也比沉默好，准备 1-2 个观点带进会议 |
| 叫 boss "Sir" / "Mr. Li" | 直接叫名字："Hui" |
| Slack 发 "Hi" 然后等回复再说正事 | 一条消息把问题说完整（No Hello: nohello.net） |
| 卡住了闷头研究两天不说话 | 卡超过 30 分钟就在 Slack 说，"I'm stuck on X, tried Y and Z, any suggestions?" |
| 等领导安排任务 | 主动找事做，完成一个立刻问 "What should I pick up next?" |
| 害怕说 "I don't understand" | 直接说，没人觉得你笨。不说、假装理解然后做错了才真的有问题 |
| 把 Code Review 意见当批评 | 这是正常流程，所有人的代码都被 review，高级工程师也一样 |

### 7.2 时区踩坑

| 踩坑行为 | 正确做法 |
|----------|---------|
| 忘了时差，在对方凌晨 @人 | 用 Slack Schedule Send，安排在对方工作时间发 |
| 日历没转换时区导致错过会议 | 所有工具设好时区，Google Calendar 开启 "Secondary time zone" |
| 把 "EOD" 理解成你的 EOD | EOD 通常指 **对方的 EOD**（美西下午 5-6 点 = 你的早上 8-9 点），不确定就问 |

### 7.3 职场文化踩坑

| 踩坑行为 | 正确做法 |
|----------|---------|
| 过度正式的邮件措辞 | 外企日常沟通偏 casual："Hey Hui, quick question..." |
| 不好意思请假 | PTO 是权利，提前说就行："I'll be OOO on Friday for personal reasons" |
| 只做被安排的事 | 主动观察、提建议。"I noticed X, what if we tried Y?" 这种主动性被高度重视 |
| 在公开场合不敢反对 | 有理有据地 disagree 是被鼓励的，"I see your point, but I think..." |

---

## 八、职业发展建议

### 8.1 前 30 天

- **第 1 周**：搞定工具、了解产品、读所有内部文档、约每个同事 1:1 了解他们的工作
- **第 2 周**：开始产出，哪怕是小的。Ship early, ship often
- **第 3-4 周**：建立节奏（Daily Standup、周报、定期 1:1），开始有自己的观点和建议

### 8.2 1:1 Meeting

定期和 leader（Hui）做 1:1，这是你最重要的沟通渠道：

- **频率**：每周一次，30 分钟
- **你主导议程**，不是 leader 主导
- **讨论内容建议**：
  - 进展和成果
  - 遇到的困难和需要的支持
  - 职业发展和学习方向
  - 对产品/策略的想法
- **主动问**："Am I meeting expectations? What can I improve?"

### 8.3 建立影响力

- 文档化你做的一切（weekly update、方案文档、复盘）
- 主动 demo 你的成果（Loom 视频、Slack 里分享）
- 在你的领域（SEO、Reddit、Content）成为团队里最懂的人
- "Your ideas matter" -- Auxora 明确说了这一点，别浪费这个文化优势

---

## 九、推荐学习资源

### 9.1 商务英语

- **Business English Pod**（Podcast）-- 每集 15 分钟场景对话
- **写作**：Grammarly 装上，日常写 Slack/邮件时实时纠错
- **阅读**：多读同事写的文档、PR description、Slack 消息，模仿他们的表达方式

### 9.2 远程工作

- 《Remote: Office Not Required》-- Basecamp 创始人写的远程工作圣经
- 《The Async-First Playbook》-- GitLab 的远程工作手册（公开免费）

### 9.3 初创公司文化

- Y Combinator 的 Startup School（免费课程）
- Paul Graham 的文章（paulgraham.com）-- 理解硅谷初创文化的底层逻辑
- Auxora 正在申请 MiraclePlus（奇绩创坛），阅读其文档理解 YC 风格的运作方式

---

## 十、Auxora 特定准备

基于你已知的 Auxora 文化和团队结构：

| Auxora 原则 | 你的行动 |
|------------|---------|
| Ship then polish | 先出 MVP 再迭代，不要追求完美才交付 |
| Blockers surface immediately | 卡住了立刻在 Slack 说，不要等 standup |
| Never promote before adding value | 先把产品用好（dogfood），再对外推广 |
| Dogfood the product | 自己用 Auxora 做自己的 GTM 工作 |
| Your ideas matter | 主动提建议，不要只执行 |

### 和团队成员的协作

- **Hui（CEO/Leader）**：你的直属。async 为主，卡住了直接 DM
- **Tingyong（廷勇，全职工程师）**：GA4 追踪需要跟他协作
- **Yuhong（裕鸿，兼职工程师）**：Agent 架构和 GTM Report 付费版
- **Yiming（奕铭，全职实习）**：PageBuilder + Creator 模块

每个人都可以直接沟通，不需要通过 Hui 中转 -- 这就是扁平化。

---

## 十一、收款与财务实操

### 11.1 收款方式对比

| 方式 | 到账速度 | 手续费 | 推荐度 |
|------|----------|--------|--------|
| **Wise** | 1-2 工作日 | ~0.5-1.5% | 首选 |
| **Payoneer** | 2-3 工作日 | 1-2% | 备选 |
| **银行电汇** | 3-5 工作日 | $15-40/笔 | 大额低频 |
| **PayPal** | 即时到账，提现 3-5 天 | 4.4%+ | 不推荐 |

### 11.2 Wise 操作流程

1. 护照注册 Wise 账户
2. 开通 USD 收款账户 -> 获得美国银行账号 + routing number
3. 把账号信息给公司，公司 ACH 转账
4. 到账后换成 CNY，提现到国内银联卡
5. 注意：偶尔触发合规审查，保留雇佣合同和 invoice

### 11.3 结汇限额

- 个人年度结汇限额 **等值 5 万美元**
- 超过需要去银行柜台，提供劳务合同、完税证明
- Wise 换汇不经过国内结汇系统，但提现到国内卡时仍占用额度
- 部分支出（SaaS 工具、VPS）直接用美元支付，减少结汇需求

### 11.4 税务

- 中国税务居民的全球收入都要缴税
- Contractor 收入属于 **劳务报酬所得**，预扣 20-40%
- 年度汇算时并入综合所得，适用 3-45% 超额累进税率
- **建议**：找懂跨境收入的会计咨询一次，保留所有合同和到账记录

---

## 十二、网络代理详细方案

### 12.1 推荐方案：自建 + 机场备用

**自建代理（最稳定）：**
- 买境外 VPS（推荐 CN2 GIA 线路，或日本/香港节点）
- 协议：VLESS + Reality（最抗封）或 Hysteria2（速度快）
- 服务端用 Xray-core 或 sing-box
- 成本约 $5-15/月

**客户端：**
- macOS：Clash Verge Rev（免费）或 Surge（付费，体验最佳）
- iOS：Shadowrocket（$2.99）

**机场（商业代理）作备用：**
- 备两家不同的，主力挂一家，另一家备用
- 不要完全依赖单一机场

### 12.2 分流配置

原则：国内直连，国外走代理。

推荐用 Loyalsoldier 的 clash-rules 订阅，自动维护国内外域名列表。

### 12.3 Git SSH 代理配置

```
# ~/.ssh/config
Host github.com
    HostName github.com
    User git
    ProxyCommand nc -X 5 -x 127.0.0.1:7897 %h %p
```

### 12.4 视频会议优化

- 代理节点选日本/香港（延迟 50-100ms）
- Hysteria2 协议对视频会议效果最好（基于 QUIC）
- 备用：手机热点 + 4G/5G（有时比家宽稳定）
- 卡顿严重就关摄像头用纯语音，美国团队一般理解

### 12.5 应急方案

- 手机 Shadowrocket 开热点给电脑用
- 至少 2 个不同线路的机场
- 紧急情况用手机 Slack 回消息，说明网络问题
