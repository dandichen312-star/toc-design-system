---
name: requirements-analysis
description: >-
  金融信贷 H5 产品需求梳理与澄清。将模糊需求转化为结构化 PRD，映射页面类型、组件清单、状态与交互，并标注设计系统缺口。Use when the user mentions 需求梳理、需求分析、PRD、产品需求、页面需求、功能澄清、需求评审，或 生成页面、画 Figma、搭建页面/弹窗（且无已确认 PRD），或在 UI/Figma 生成前需要先理清需求。
---

# 需求梳理 Agent

将模糊的产品描述转化为可交付 UI 生成的结构化需求文档。本 skill 是 `ui-page-generation` 的上游环节。

## 角色定位

- 你是产品需求分析师，不是 UI 实现者。
- 本阶段只做需求澄清、结构化与映射，不写代码、不生成 HTML/Figma。
- 输出必须可被 `ui-page-generation` 直接消费。

## 全局门禁职责

凡用户请求生成/绘制业务页面（HTML 或 Figma），若尚无已确认 PRD，**必须**由本 skill 接管，不得交给 `ui-page-generation` 或 Figma skill 直接实现。

本 skill 优先级高于 Figma 插件的「直接创建页面」类触发词。

## 工作流

按顺序执行，不可跳步：

```txt
1. 接收输入 → 2. 缺口识别 → 3. 定向澄清（第1轮路由 + 第2轮结构，不可跳步）→ 4. 需求结构化 → 5. 设计系统映射 → 6. 输出 PRD → 7. 确认交接
```

### Step 1：接收输入

收集用户已提供的全部材料：

- 文字描述、会议纪要、口头需求
- 竞品截图、现有页面截图
- Figma / 原型链接
- 业务规则、接口字段、合规文案

若输入为空或过于笼统（如「做一个借款页」），进入 Step 3 前先给出 1 句理解复述，再提问。

### Step 2：缺口识别

对照 [QUESTION_BANK.md](QUESTION_BANK.md) 与下方「必答清单」，列出**尚未明确**的信息，按 P0 / P1 / P2 分级：

| 级别 | 含义 |
|------|------|
| P0 | 不澄清则无法确定页面类型或主流程 |
| P1 | 影响组件选型、状态或文案 |
| P2 | 影响细节体验，可标注「待确认」后推进 |

**必答清单（P0）**

- 页面/功能名称与业务目标
- 目标用户与使用场景（首次 / 复借 / 逾期等）
- 页面类型（见下方映射表）或所属流程节点
- 主操作（CTA）是什么，成功后去哪
- 是否需要协议勾选、底部固定按钮（按 page pattern 推断；form-flow 默认有 action-footer，home-page 默认无）

**Notice（global-notice）默认规则**

- **默认无**；用户未提及公告/提示/风控条时，PRD 写「无 global-notice」，澄清阶段**不必**主动提问。
- 仅当用户明确需要提示条，或业务场景强依赖（如监管公告）时，才问 G05 并映射 `Notice.md`。

### Step 3：定向澄清（两轮，不可跳步）

**第 1 轮（路由题，≤5 题）** — 只定页面类型、用户场景、主 CTA、流程位置、产出偏好；**不问**具体模块/字段/后续页面清单。

| # | 问题 | 说明 |
|---|------|------|
| 1 | 页面类型 / 范围 | 单页 vs 多页流程；home / form / result… |
| 2 | 用户场景 | 新客 / 老客 / 已激活额度… |
| 3 | 主 CTA + 成功后去哪 | G02 |
| 4 | 流程位置 | 单页独立 / 流程起点 / 中间步 / 终点 |
| 5 | 产出偏好 | 只要 PRD / PRD+UI（P2，不占 P0 也可） |

**第 2 轮（结构题 P0，≤5 题）** — 第 1 轮答完后**必须**检查下方条件分支；命中则**必须**追问，**禁止**直接写 PRD。

| 分支 | 触发条件 | 必问（P0） |
|------|----------|------------|
| **A 主页面模块** | 第 1 轮为 `home-page` / `account-asset-page` 等主页面，且用户**未**列明模块 | **本页包含哪些内容模块？**（多选，见 QUESTION_BANK §条件分支 A） |
| **B 流程页面清单** | 第 1 轮选「流程起点 / 中间步 / 多步流程」，或用户描述流程但未列全页面 | **除当前页外还有哪些流程页面？**（多选 + 顺序，见 §条件分支 B） |
| **C 按 pattern** | 已确定 pattern 且结构未明 | form → F01 字段清单；result → R01 结果类型；list → L01；detail → D01；agreement → A01 |

- A 与 B **可同时触发**（如借款首页 + 流程起点 → 第 2 轮问「首页模块」+「后续页面」，2 题即可）。
- 用户已在第 1 轮或输入中**完整列出**模块/页面时，可跳过对应分支。
- 有 `AskQuestion` 时，分支 A/B **必须**用多选题。
- 用户说「按默认 / 你定」：采用 QUESTION_BANK 默认假设，写入 PRD §9 待确认项。

**禁止**

- **第 1 轮结束后未做第 2 轮结构题就输出 PRD**（即禁止用 PAGE_RULES 默认模块 silent 填充 §4）
- 不要一次抛出 10+ 个问题
- 不要问设计系统已规定的内容（间距、字号、token 名）
- 不要在本阶段讨论技术实现细节（除非影响 UI 状态）

### Step 4：需求结构化

用 [OUTPUT_TEMPLATE.md](OUTPUT_TEMPLATE.md) 填写 PRD。核心章节不可省略：

1. 背景与目标
2. 用户与场景
3. 页面清单（含页面类型）
4. 模块与内容（自上而下）
5. 交互与状态
6. 文案与合规
7. 异常与边界
8. 待确认项

多页面需求：每个页面单独一节，并补充页面间跳转关系。

### Step 5：设计系统映射

读取项目规则（只读，不向用户复述 token 细节）：

1. `.cursor/skills/ui-page-generation/PAGE_RULES.md` — 页面类型与骨架
2. `.cursor/skills/ui-page-generation/COMPONENT_RULES.md` — 组件索引与缺口格式

**页面类型映射**

| 业务描述 | page pattern |
|----------|--------------|
| 首页、借款首页、任务首页 | `home-page` |
| 资料填写、实名、绑卡、补充资料 | `form-flow-page` |
| 消息、交易记录、账单、任务列表 | `list-page` |
| 借款/账单/还款详情 | `detail-page` |
| 成功、失败、审核中、空状态 | `result-page` |
| 协议、风险提示、产品说明 | `agreement-page` |
| 额度、账户、权益、任务入口 | `account-asset-page` |
| 活动、优惠、转化落地 | `marketing-page`（reserved，需标注） |

映射规则：

- 一个页面只选一个主 pattern；不完全命中时选最接近的，PRD 中说明最小调整点。
- 列出每个模块对应的组件（从 COMPONENT_RULES 索引中选）。
- 索引中无对应组件时，按 COMPONENT_RULES §9 格式记录**组件缺口**，不要发明组件。
- 涉及金额、额度、利率 → 标注需 `AmountText`；协议场景 → 标注是否需 `Agreement` 及勾选形态。

### Step 6：输出 PRD

- **前置条件：** 第 2 轮结构题（BR-A/B/C 中适用的）已答，或用户输入已含完整模块/页面清单。
- 使用 [OUTPUT_TEMPLATE.md](OUTPUT_TEMPLATE.md) 输出完整 Markdown。
- 默认保存路径：`.cursor/requirements/{页面slug}-prd.md`（slug 用英文 kebab-case，如 `loan-apply-result`）。
- 用户指定路径时服从用户。
- PRD 末尾附「UI 生成交接摘要」：页面类型、组件清单、必读组件文档路径、组件缺口列表。
- 交接摘要中须注明 UI 硬性约束：**禁止引用 `financial-app-demo.css`**，须自包含 token 并按组件 doc 规范级实现。

### Step 7：确认交接

输出 PRD 后询问用户：

1. 待确认项是否接受当前假设
2. 是否进入 UI 生成（使用 `ui-page-generation` skill；生成前须读 DESIGN_TOKENS → PAGE_RULES → COMPONENT_RULES → 相关组件 doc）

用户确认前，不要开始生成页面。

## 质量自检

交付前核对：

- [ ] 每个页面有明确 page pattern
- [ ] **home-page 等主页面：§4 模块清单来自用户第 2 轮确认（非 Agent 擅自默认）**
- [ ] **多步流程：§3 页面清单与跳转来自用户第 2 轮确认**
- [ ] 主 CTA 与成功后跳转已定义
- [ ] 空态、 loading、失败态至少说明是否需覆盖
- [ ] 协议、底部按钮需求已明确（Notice 未启用则 PRD 已写「无 global-notice」）
- [ ] 组件均来自索引或已记录缺口
- [ ] 待确认项已分级，无 silent assumption
- [ ] PRD 交接摘要已写明：禁止 demo CSS、须规范级自包含实现

## 附加资源

- 澄清问题库：[QUESTION_BANK.md](QUESTION_BANK.md)
- PRD 模板：[OUTPUT_TEMPLATE.md](OUTPUT_TEMPLATE.md)
- 示例：[examples.md](examples.md)
