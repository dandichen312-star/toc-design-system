# RepaymentPlan（还款计划）

## 1. 用途与边界

RepaymentPlan 用于展示按期还款计划，适用于还款计划弹窗、还款详情页、借款详情中的分期还款信息等场景。

RepaymentPlan 负责：

- 展示按期还款的期数、还款日期和每期金额。
- 展示纵向时间轴节点和连线。
- 在需要时展示计划下方的息费规则说明。

RepaymentPlan 不负责：

- 不负责借款金额输入、编辑和校验。
- 不负责切换还款方式、筛选期数或分页。
- 不负责弹层容器本身；如果出现在弹窗中，弹窗规则仍遵循 `ModalPopup.md`。
- 不替代通用 `List`、`Card` 或 `Notice` 的页面级容器规则。

---

## 2. 组件结构

```txt
RepaymentPlan
├── plan-list
│   └── plan-item 可重复
│       ├── installment-meta
│       │   ├── installment-label
│       │   └── installment-date
│       ├── timeline-axis
│       │   ├── timeline-dot
│       │   └── timeline-connector optional
│       └── installment-content
│           ├── installment-amount
│           └── installment-note optional
└── fee-rule optional
    ├── fee-rule-title
    └── fee-rule-text 可重复
```

规则：

- `plan-list` 为单列纵向结构，一条数据对应一个 `plan-item`。
- `plan-item` 固定由三列组成：左侧期数信息、中间时间轴、右侧每期金额。
- 左侧 `installment-meta` 负责展示“首期 / 2期 / 3期”这类期数标签，以及对应日期。
- 中间 `timeline-axis` 负责展示节点和上下连线。
- 右侧 `installment-content` 负责展示每期应还金额，以及金额下方的补充说明文案。
- `fee-rule` 为可选说明区，默认放在还款计划列表下方。

---

## 3. 布局规则

```txt
width:
  fill / 跟随当前内容区宽度

plan-list:
  width: fill

plan-item:
  width: fill
  layout: horizontal

fee-rule:
  width: fill
```

规则：

- RepaymentPlan 默认占满当前内容区可用宽度，跟随页面或弹层内容区自适应。
- `plan-item` 使用横向布局，左侧期数信息、中间时间轴、右侧金额按列排布。
- 左侧期数信息为固定内容列，中间时间轴为固定视觉列，右侧金额为内容列。
- `installment-meta` 内部使用纵向排列：期数在上，日期在下。
- 金额列与当前期节点在同一行对齐。
- 多个 `plan-item` 纵向连续排列，时间轴连线在相邻期数之间自然衔接。
- `fee-rule` 与 `plan-list` 之间默认使用 `spacing-32`。
- 息费规则说明区默认左对齐，占满组件可用宽度。

---

## 4. 内容规则

### 4.1 期数信息

规则：

- `installment-label` 用于展示“首期 / 2期 / 3期”这类期数名称。
- `installment-date` 用于展示对应还款日期，如 `01/28`。
- 第一版还款计划最多支持 `12` 期展示。
- 超过 `12` 期的场景不在当前组件默认支持范围内，不能由 AI 自行扩展为更多期数结构。
- 日期属于数字信息，数字字符应使用 `font-family-number`。
- 期数标签与日期为同一组元信息，必须上下相邻展示，不拆到不同区域。

### 4.2 每期金额

规则：

- `installment-amount` 属于金融金额信息，必须遵循 `AmountText.md`。
- 每期金额默认使用普通金额色，不默认使用营销高亮色。
- 金额中的数字字符必须使用 `font-family-number`。
- 金额默认单行展示，不允许折行。
- 若业务文案要求带 `¥`，则金额展示遵循 `AmountText.md` 中允许带符号的规则。
- 每期金额下方允许出现 `installment-note` 说明文案，用于表达本金、利息、担保费等拆分信息。
- `installment-note` 为可选，不要求每一期都必须出现。
- `installment-note` 默认紧跟在对应金额下方，不单独换到其它区域。

### 4.3 息费规则说明

规则：

- `fee-rule` 为可选区块，不强制每个 RepaymentPlan 都出现。
- 出现时，默认结构为“标题 + 多行正文说明”。
- `fee-rule-title` 用于展示类似“息费规则说明”的区块标题。
- `fee-rule-text` 用于展示利率、综合资金成本、出资机构等说明文案。
- 息费规则说明区是正文说明，不作为公告条，不使用 `Notice` 形态。

---

## 5. 视觉与 Token 使用

```txt
期数标签：
  text-body-md
  color-text-primary

日期：
  text-body-sm
  color-text-secondary

每期金额：
  遵循 AmountText.md

每期金额说明：
  text-body-sm
  color-text-tertiary

时间轴节点：
  color-text-secondary / color-border-default

时间轴连线：
  color-border-subtle

息费规则标题：
  text-title-sm
  color-text-primary

息费规则正文：
  text-body-sm
  color-text-secondary

组件宽度：
  fill / 100%

与下方说明区间距：
  spacing-32
```

规则：

- RepaymentPlan 的字色、字号、间距必须优先使用 `DESIGN_TOKENS.md` 中已有 token。
- 时间轴节点和连线属于组件内部结构表现，不额外创建独立图标组件文档。
- 未经确认，不在本组件中新增卡片底色、描边或特殊背景。
- 如果 RepaymentPlan 被放进 `Card` 或弹层正文，外层容器背景由页面或容器组件决定，不由 RepaymentPlan 自行定义。

---

## 6. 使用场景规则

```txt
适用场景：
  还款计划弹窗
  还款详情页
  借款详情中的分期还款计划区
```

规则：

- 当页面中出现“按期列表 + 日期 + 每期金额 + 纵向时间轴”的结构时，必须优先识别为 `RepaymentPlan`。
- 当页面中出现“按期列表 + 日期 + 每期金额 + 金额下补充说明 + 纵向时间轴”的结构时，仍然归入 `RepaymentPlan`，不新增第 2 个组件。
- RepaymentPlan 可以出现在详情页正文，也可以出现在弹窗正文。
- 出现在弹窗中时，RepaymentPlan 只负责正文内容，不改写弹层头部、底部按钮或关闭规则。
- 当 RepaymentPlan 出现在弹窗中，且 `plan-list + installment-note + fee-rule` 累计高度超过弹窗正文最大高度时，必须由弹窗正文区滚动展示；标题区和关闭按钮保持固定。
- 出现在详情页时，RepaymentPlan 默认跟随正文流展示，不默认吸底。

---

## 7. AI 使用规则

- AI 不允许用普通 `List + 文本 + 手工圆点 + 手工连线` 临时拼装替代 RepaymentPlan。
- AI 不允许把单条还款计划拆成多个无关组件分别生成。
- 当页面同时存在“还款计划列表”和“息费规则说明”且两者属于同一业务块时，优先作为一个 `RepaymentPlan` 区块处理。
- 第一版默认只支持 `1-12` 期范围内的还款计划展示。
- 如果页面只有息费说明，没有期数时间轴列表，不使用 RepaymentPlan。
- 如果页面只有普通信息列表，没有期数时间轴结构，不使用 RepaymentPlan。
