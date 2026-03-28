# Repository Guidelines

## 项目定位
这是 Auxora.ai 的 GTM 工作区，不是应用代码仓库。仓库主要保存研究、计划、审计报告和对外分享材料。当前产品背景如下：

- 产品：Auxora.ai，面向美国个体创业者的 AI marketing engine
- 主要内容类型：研究笔记、执行计划、产品诊断、SEO 审计、截图素材
- 当前没有应用构建流程，也没有测试框架

涉及产品状态或 GTM 判断时，默认以仓库内最新文档为准；不要把这里当作代码项目处理。

## 目录结构
- 根目录：少量顶层研究素材和代理配置文件，例如 `info.md`、`calder_onboarding.pdf`、`AGENTS.md`、`CLAUDE.md`
- `docs/plans/`：核心工作文档，包含 `feat`、`report`、`guide` 三类文件；以 Markdown 为主，必要时可有 `.docx`
- `docs/screenshots/`：文档引用的截图素材

新增文档优先放在 `docs/` 下，不要随意增加新的顶层目录。

注意：

- 根目录若出现 `.png`，视为历史遗留副本；新文档不要引用这些文件
- 截图统一引用 `docs/screenshots/` 下的文件
- 不要提交无意义的系统文件，例如 `.DS_Store`

## 文件命名
计划、报告、指南统一使用：

`YYYY-MM-DD-type-topic.md`

约定如下：

- `type` 仅使用 `feat`、`report`、`guide`
- 文件名使用小写和连字符
- 主题名保持简短可读，不做未来扩展预留

示例：

- `2026-03-25-report-case-a-pro-diagnosis.md`
- `2026-03-25-feat-case-bc-testing-plan.md`

如果需要对外分享的 Word 文档，可沿用同名 `.docx`，与对应的 `.md` 放在同一目录。

## 文档格式
`docs/plans/` 下的计划类和报告类文件默认包含 YAML frontmatter：

```yaml
---
title: 标题
type: report | feat | guide
date: YYYY-MM-DD
author: Name
audience: Name (Role)
---
```

正文约定：

- 全部文档默认使用中文；没有自然中文对应的技术词可保留英文
- 标题层级使用标准 Markdown `#` / `##`
- 段落简短，列表保持单层
- 以业务可读性优先，避免写成代码注释风格
- 控制篇幅，优先保留结论、证据、建议和下一步

## 图片与链接
截图引用必须使用相对路径，不要使用绝对路径，也不要使用 raw GitHub URL。

正确示例：

```md
![登录页面](../screenshots/free-login-page.png)
```

新增截图时：

- 文件放入 `docs/screenshots/`
- 文件名使用小写连字符
- 文档内先确认相对路径能正常渲染

## 常用检查命令
仓库没有 build pipeline。修改后用轻量命令自查：

```bash
rg --files .
find docs -maxdepth 2 -type f | sort
find docs/plans -name '*.md' | sort | tail -5
sed -n '1,160p' docs/plans/<filename>.md
```

## 提交前检查
没有自动化测试时，人工校验就是最低标准。提交前至少确认：

- Markdown 能正常渲染
- frontmatter 字段完整且日期正确
- 文中日期、负责人、交付物前后一致
- 截图路径可用，且引用的是 `docs/screenshots/` 中的文件
- 没有误引用根目录历史遗留图片
- 没有新增 `.DS_Store`、凭证或内部敏感信息

如果本次变更引入脚本或代码，再把对应验证命令补充到本文件。

## Git 与提交约定
该仓库已有提交历史，当前提交风格使用 `docs:` 前缀。默认遵循：

- 提交信息简短、祈使句、聚焦单一文档或单一决策
- 优先使用 `docs:` scope

示例：

- `docs: tighten case a diagnosis report`
- `docs: sync agents guidance with repo conventions`

Pull Request 描述应说明：

- 这次改动解决什么问题
- 改了哪些文件
- 是否有后续待确认事项
- 若更新了视觉素材，附上必要截图

## 内容安全
不要提交以下内容：

- 凭证、密钥、Cookie、账号信息
- 私有客户数据或外部系统复制来的内部备注
- 未确认可公开传播的运营数据

大文件和二进制素材只在确有必要时加入；能在文档中引用来源的，优先引用来源。
