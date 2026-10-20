---
name: repo-docs-system
description: |
  Build and maintain a structured Chinese knowledge base (docs/ system) for any code repository.
  Use this skill whenever: the user wants to init docs for a project, write AGENTS.md,
  create ARCHITECTURE.md, set up a docs/ directory, update product-specs or exec-plans,
  generate a QUALITY_SCORE.md report, or mentions "knowledge base", "design docs",
  "product specs", "exec plans". Also use when the user wants AI agents to better
  understand their project structure. Trigger even for requests like "organize my project docs",
  "build a docs system", "help me document this codebase", or "create an AGENTS.md file".
---

# 仓库知识库文档体系 Skill

## 概述

本 Skill 帮助你为任意代码仓库构建一套**结构化的中文知识库**，以 `docs/` 目录为核心记录系统，以 `AGENTS.md` 作为注入上下文的"地图文件"。

核心职责：
1. **初始化**：从零生成完整 `docs/` 目录结构，内容贴近项目真实情况
2. **维护更新**：为已有体系增补或更新特定文档
3. **质量评分**：生成/刷新 `QUALITY_SCORE.md`，追踪覆盖缺口

> **所有输出文档必须使用中文。**

---

## 执行流程

### 第一步：快速探索代码库（不要过度阅读）

阅读以下内容（每项快速浏览）：

1. 根目录的 `README.md`、`package.json` / `pyproject.toml` / `go.mod` 等依赖清单
2. 顶层目录结构
3. 已有的 `docs/` 目录（如果存在）
4. 关键入口文件（各读前 50 行即可）

目标：理解**技术栈、架构层次、核心域、主要功能模块**。理解到能写出准确文档就够了，然后**立即开始输出文件**。

---

### 第二步：与用户确认关键边界（仅在必要时）

遇到以下情况才用 `AskUserQuestion` 确认，其他先假设后标注：

- 产品域划分不明确时
- 用户没有明确说要生成哪些子目录时（询问是否全量生成）

对于细节性不确定，自行假设并用 `> ⚠️ 待确认：…` 标注。

---

### 第三步：按优先级顺序输出文件

**严格按以下顺序**生成，确保最重要的文件先完成：

1. `AGENTS.md` ← 最重要，**先生成**
2. `ARCHITECTURE.md`
3. `docs/design-docs/core-beliefs.md`
4. `docs/design-docs/index.md`
5. `docs/product-specs/index.md`
6. `docs/exec-plans/tech-debt-tracker.md`
7. `docs/QUALITY_SCORE.md`
8. `docs/SECURITY.md`、`docs/RELIABILITY.md`、`docs/PLANS.md`（按需）

根据项目真实情况裁剪，不要机械复制结构。

---

### 文档内容规范

#### AGENTS.md（最重要，约 80-120 行）

```markdown
# {项目名} — Agent 上下文地图

> 最后更新：{日期}

## 项目概述
（1-2 句话）

## 技术栈
| 层次 | 技术 |
|------|------|

## 架构速览
（指向 ARCHITECTURE.md）

## 文档导航
| 文档 | 用途 | 路径 |
|------|------|------|
| 架构设计 | 域划分与包分层 | ARCHITECTURE.md |
| 设计文档 | 技术决策记录 | docs/design-docs/index.md |
| 产品规范 | 功能需求详情 | docs/product-specs/index.md |
...

## 关键约定
（命名约定、禁忌事项）

## 常见任务指引
（新增 API / 修改数据库 / 新增功能 → 分别指向对应文档）
```

#### docs/design-docs/index.md

**必须使用 emoji 验证状态标记**：
- ✅ 已验证（与代码一致）
- 🔄 草稿（撰写中）
- ❓ 待验证（未核对）
- ❌ 已过时

#### docs/QUALITY_SCORE.md

评分维度（0-5 分）：覆盖率、内容完整度、交叉引用完整性

**必须包含历史趋势表格**：
```markdown
## 历史趋势
| 日期 | 整体评分 | 主要改进 |
|------|---------|--------|
| {日期} | X.X/5 | 初始化 |
```

---

### 第四步：维护模式（已有 docs/ 时）

1. **不要删除**已有内容，只新增或更新
2. 必须重新生成 `AGENTS.md`（保持索引最新）
3. 更新 `QUALITY_SCORE.md` 评分，并追加历史趋势行

---

## 写作规范

- **语言**：全部中文，专有名词（框架名、库名、API 名）保留英文
- **格式**：Markdown，善用表格、列表、代码块
- **占位符**：用 `{待填写：xxx}` 表示需要用户补充的信息
- **待确认**：用 `> ⚠️ 待确认：xxx` 标注推断性内容
