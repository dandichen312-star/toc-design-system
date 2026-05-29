---
name: ui-page-generation
description: >-
  金融信贷 H5 规范级页面生成。按 DESIGN_TOKENS、PAGE_RULES、COMPONENT_RULES 与组件文档实现页面。
  Use when the user mentions UI 生成、生成页面、H5 页面、绑卡页、表单页、首页、按规范实现、
  ui-page-generation，或在 PRD 已确认后需要产出 HTML/Figma 页面。
---

# UI 页面生成

按项目设计系统**规范级**生成 Mobile / H5 页面。本 skill 是 `requirements-analysis` 的下游环节。

## 前置门禁（不可跳过）

- 无已确认 PRD 时，**不得**执行本 skill 的任何步骤。
- 先完成 `requirements-analysis`，PRD 保存至 `.cursor/requirements/{slug}-prd.md` 且用户确认后，才可进入本 skill。
- 用户要求 Figma 出图时同样适用：**先 PRD，后 Figma**。
- 多页面流程共用一个 PRD（如 `loan-flow-prd.md`），不要拆成多个文件绕过检查。

## 硬性约束（不可违反）

### 禁止引用 demo 样式

- **禁止**在生成的 HTML 中 `<link>` 或 `@import` `financial-app-demo.css`。
- **禁止**复用 `financial-app-demo.html` 中的 class 命名、布局习惯或组件结构作为实现依据。
- `financial-app-demo.*` 仅作历史演示参考，**不是**设计系统 source of truth。

### 必须自包含实现

每个页面产出必须：

1. 在页面 CSS 中声明完整语义 token（颜色、字号、间距、圆角、阴影等），值来自 `DESIGN_TOKENS.md`。
2. 按组件文档实现 DOM 结构与样式，不得用临时 class 模拟已有组件。
3. HTML / CSS / JS 分离或单文件均可，但样式与结构必须能独立运行、不依赖 demo 全局样式。

### 生成前必读顺序

严格按序读取，不可跳步：

```txt
1. DESIGN_TOKENS.md
2. PAGE_RULES.md — 确认页面类型与 pattern 章节
3. COMPONENT_RULES.md
4. 当前页面 PRD（必须）— .cursor/requirements/*-prd.md，状态为「已确认」或用户在本对话已批准
5. 按需读取组件文档 — docs/components/*.md
```

### 生成后自检

交付前逐项核对：

- [ ] 未引用 `financial-app-demo.css` 或 demo 专用 class
- [ ] token 均可在 `DESIGN_TOKENS.md` 中找到来源
- [ ] 页面 skeleton 符合 `PAGE_RULES` 对应 pattern（如 `form-flow-page`）
- [ ] 每个 UI 模块对应 COMPONENT_RULES 索引中的组件（Header / Form / FormItem / Input / Notice / Button / Toast / PickerSheet 等）
- [ ] Form 表单项使用文档规定的 `field-row-group`、`left-area` / `right-area` / `suffix` 结构
- [ ] **global-notice**：仅当 PRD 明确启用时绘制，且布局符合 `PAGE_RULES` §8；PRD 未启用则页面**不得**出现 Notice
- [ ] 主按钮位置符合页面类型（表单页用 `action-footer`，非首页不吸底混排）
- [ ] 未临时发明组件变体；缺口已按 `COMPONENT_RULES` §9 记录

## 工作流

```txt
1. 读取 PRD 或用户描述 → 确认 page pattern 与组件清单
2. 按「生成前必读顺序」加载规则与组件文档
3. 搭建页面 skeleton（Page → header → content-layer → action-footer）；**无 PRD 指定的 global-notice 时不加 Notice 模块**
4. 逐模块按组件 doc 实现结构与 token
5. 补充交互状态（loading / empty / error / Toast / PickerSheet 等 PRD 要求的状态）
6. 执行「生成后自检」后再交付
```

## 参考实现（结构模式，非样式依赖）

需要对照「规范级 HTML 结构」时，优先参考项目中已按本 skill 实现的页面（如 `financial-homepage.html`、`bind-bank-card.html`），**只学结构与 token 组织方式**，不要复制 demo 文件做法。

## 附加资源

- 页面规则：[PAGE_RULES.md](PAGE_RULES.md)
- 组件索引：[COMPONENT_RULES.md](COMPONENT_RULES.md)
- 设计 token：[DESIGN_TOKENS.md](DESIGN_TOKENS.md)
- 上游 PRD：`.cursor/requirements/`
