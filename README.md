# PRD Kit

Create business-readable PRDs for cross-functional teams. PRD Kit helps product, operations, marketing, partners, and engineering align on confirmed business rules, scope, acceptance criteria, risks, and open decisions.

## Modes

- **Mode 1 - Framework first:** use guided questions to settle a larger product framework before turning it into an implementation-ready PRD.
- **Mode 2 - Direct PRD:** turn available facts into a review-ready PRD and ask only for missing high-impact decisions.

## Use

Install the skill under your Codex skills directory, then invoke it with `$prd-kit`. By default, generated resources are written to `<current-working-directory>/<project-slug>/`; specify an output directory in the request to override it.

PRD Kit creates a review draft by default. It synchronizes an external parent work item only when explicitly requested.

---

## 中文介绍

面向产品、运营、市场、合作团队与研发的跨部门 PRD skill。PRD Kit 将已确认的业务口径、范围、验收标准、风险和待确认事项整理为所有角色都能阅读的 PRD。

## 两种模式

- **模式 1 - 先定框架：** 先通过引导式提问确定较大的产品框架，再进入可开发的 PRD。
- **模式 2 - 直接产出：** 基于已有事实生成可评审 PRD，只追问缺失的高影响决策。

## 使用方式

将 skill 安装到 Codex skills 目录后，通过 `$prd-kit` 调用。默认资源目录为 `<当前工作目录>/<项目-slug>/`；可在请求中明确指定输出目录。

默认只生成复核草案；仅在明确要求时同步外部父工作项。
