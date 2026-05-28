# Card 卡片

## 1. 用途

Card 用于承载一组相关信息，例如额度信息、营销权益、表单分组、提示内容、列表区块、详情信息等。

Card 表达内容分组，不用于单纯制造间距。

## 2. 类型

```txt
default：普通信息承载。
highlight：重点营销、权益、优惠、强提醒内容。
interactive：可点击入口、选择项、详情入口或轻量操作入口。
```

AI 选择规则：

- 普通信息分组、表单分组、详情信息、列表区块：使用 `default`。
- 营销权益、优惠、重点提示、需要视觉强调的内容：使用 `highlight`。
- 可点击入口、选择项、详情入口：使用 `interactive`。

## 3. 内容结构

```txt
Card:
  header 可选
    title 必填
    extra / action 可选

  body 必填
    content

  footer 可选
    action / remark
```

规则：

- `header` 用于标题、辅助操作、右侧说明。
- `body` 承载卡片核心内容，必须存在。
- `footer` 用于底部按钮、协议说明、补充备注，不要承载主内容。
- 当 Card 所属模块已经有页面区块标题时，标题应放在 Card 外部，Card 内不重复使用 `header.title`。
- 卡片内只放同一主题的信息。
- 卡片标题应简短明确，避免超过一行。
- 卡片内主次信息必须有清晰层级。

## 4. 尺寸与布局

```txt
width:
  默认跟随父容器宽度
  H5 页面内通常占满内容区宽度

height:
  default: auto / hug content
  summary: auto，必要时设置 min-height
  benefit: 同组卡片必须统一高度
  task-list: auto，由列表项数量决定
  product: auto，由产品项数量决定

layout:
  vertical: 默认布局，内容上下排列
  horizontal: 左右布局，用于入口卡、列表项、小型信息卡

padding:
  default: spacing-card-padding
  vertical-large-y: 32px
  horizontal-y: 20px
  list-card-y: 20px

gap:
  header-body: spacing-list-gap
  content-item: spacing-list-gap
  card-card: spacing-section-gap
  compact-card-column-gap: spacing-8

radius:
  radius-card = radius-8 = 8px

shadow:
  default: shadow-none
  highlight / interactive 可按页面层级使用 shadow-sm
```

规则：

- Card 不直接决定页面左右边距，页面容器负责外边距。
- Card 默认高度由内容撑开，不统一写死高度。
- 只有同组并排展示的 `benefit` 卡片可以统一高度。
- `task-list` 外层 Card 高度由列表项数量决定。
- `product` 外层 Card 高度由产品项数量决定。
- 单列垂直大卡使用 `vertical-large-y: 32px` 作为上下内边距。
- 多列 `vertical-compact` 小卡保持紧凑内边距，不跟随单列大卡的 `32px` 上下内边距。
- 单个左右布局卡使用 `horizontal-y: 20px` 作为上下内边距，高度由内容撑开。
- 多个左右布局行组合成一个 `list-card` 时，外层 Card 使用 `list-card-y: 20px` 作为上下内边距，高度由列表项数量撑开。
- Card 默认使用 `vertical` 布局。
- `horizontal` 用于入口卡、列表项、小型信息卡。
- 如果 Card 内部包含多个列表项，外层 Card 使用 `vertical`，内部列表项使用 `horizontal`。
- Card 内部使用 auto layout 组织内容。
- 多个 Card 之间使用 `spacing-section-gap`。
- 同一卡片内部的信息项之间使用 `spacing-list-gap`。
- 2 列 / 3 列并排小卡之间使用 `spacing-8`。
- 所有 Card 默认统一使用 `radius-card`，即 `radius-8` / 8px。
- 不允许根据卡片大小临时调整圆角。
- 不要用空白 Card 或嵌套 Card 制造间距。

## 5. 内部间距

```txt
section-gap:
  header-body: spacing-list-gap
  body-footer: spacing-list-gap

item-gap:
  title-subtitle: spacing-4
  amount-label-amount: spacing-4
  metric-label-metric: spacing-4
  item-item: spacing-list-gap
  list-item-gap: spacing-0

inline-gap:
  icon-content: spacing-8
  content-action: spacing-12
  metric-metric: spacing-12

action-gap:
  content-button: spacing-list-gap

density-gap:
  vertical-large-content-action: spacing-32
  vertical-compact-content-action: spacing-16
```

布局规则：

```txt
vertical:
  header / body / footer 之间使用 section-gap
  标题与说明之间使用 title-subtitle
  金额名称与金额之间使用 amount-label-amount
  内容与按钮之间使用 content-button

vertical-large:
  用于整行大卡、页面核心额度卡、主视觉卡
  padding-top: 32px
  padding-bottom: 32px
  主内容与按钮之间使用 vertical-large-content-action

vertical-compact:
  用于 2 列 / 3 列权益小卡、并排小卡
  padding-y: compact default
  主内容与按钮之间使用 vertical-compact-content-action

horizontal-task:
  padding-top: 20px
  padding-bottom: 20px
  icon 与文字区之间使用 icon-content
  标题与次标题之间使用 title-subtitle
  文字区与按钮之间使用 content-action

horizontal-product:
  padding-top: 20px
  padding-bottom: 20px
  产品信息与指标区之间使用 content-action
  指标之间使用 metric-metric
  指标区与按钮之间使用 content-action

list-card:
  applies-to: task-list / product-list
  layout-mode: vertical auto-layout
  width: fill / parent-defined
  padding-top: 20px
  padding-bottom: 20px
  item-gap: spacing-0
  item-separator: divider
  separator-gap-y: spacing-16

horizontal-row:
  layout-mode: horizontal auto-layout
  width: fill
  leading: fixed
  content: fill
  trailing-action: fixed
  divider: fill
```

规则：

- Card 内部间距按元素关系定义，不按业务卡片逐个写死。
- 小关系使用 `spacing-4`，例如标题与说明、金额名称与金额。
- 小关系必须按上一个元素底边计算：`next.y = previous.y + previous.height + spacing-4`。
- 不允许凭视觉手调标题与说明、金额与金额说明、指标值与指标说明之间的距离。
- 默认关系使用 `spacing-8`，例如图标与内容、列表项之间。
- 强分组关系使用 `spacing-12`，例如内容区与操作区、多个指标之间。
- `layout` 决定排列方向，`density` 决定同一布局下的间距大小。
- `vertical-large` 仅用于单列大卡；它的上下内边距使用 `32px`。
- `vertical-compact` 虽然也是垂直内容结构，但用于多列小卡，不使用 `vertical-large` 的 `32px` 上下内边距。
- 单个 `horizontal-task` / `horizontal-product` 卡片的上下内边距使用 `20px`，高度必须由内容撑开。
- `vertical-large` 的主内容到按钮间距使用 `spacing-32`。
- `vertical-compact` 的主内容到按钮间距使用 `spacing-16`。
- `task-list` / `product-list` 属于列表型 Card，外层上下内边距使用 `20px`，顶部留白必须等于底部留白。
- `task-list` / `product-list` 必须使用 Auto Layout，不允许用固定 x / y 坐标堆叠列表项。
- 左右布局的列表行必须使用横向 Auto Layout：leading 固定宽度，content 使用 fill，trailing-action 固定宽度。
- 分割线宽度必须使用 fill，随 Card 内容宽度变化。
- 列表型 Card 的第一个列表项从顶部 padding 后开始，最后一个列表项结束后必须保留同等底部 padding。
- 列表项数量大于 1 时必须使用分割线，不使用大间距区分列表项。
- 分割线与上下列表项内容之间统一使用 `spacing-16`。
- Card 外部与其他模块的间距由父容器控制，不写在 Card 内部。

## 6. 卡片操作与金额规则

```txt
vertical-large:
  amount: AmountText large / hero
  amount-weight: bold
  default-action-count: 1

  single-action:
    button-size: xlarge
    button-height: 54px
    button-width: full

  double-action:
    button-size: xlarge
    button-width: equal
    button-gap: spacing-12
    usage: 仅当业务明确存在两个同级操作时使用

vertical-compact:
  title: font-size-20 / line-height-28
  amount-weight: medium
  2 columns button-height: 32px
  3 columns button-height: 28px
  button-width: fill
  content-action-gap: spacing-16
  column-gap: spacing-8

horizontal:
  amount-weight: medium
  metric-weight: medium
  trailing-action:
    button-size: small
    button-width: fixed
    button-width-value: 64px
    button-height: 32px
    align: right
```

规则：

- Card 不默认生成两个按钮；未明确双操作时，默认只生成一个主按钮。
- `vertical-large` 的核心金额必须使用 AmountText `large` 或 `hero`，不得使用普通标题字号。
- `vertical-large` 单列大卡中的核心金额使用粗体 `bold`，用于建立页面主视觉层级。
- 除 `vertical-large` 单列大卡外，Card 内其他金额、额度、利率和指标数字默认使用中粗 `medium`，不与首页主金额抢层级。
- `vertical-large` 单按钮宽度撑满卡片可用内容区。
- `vertical-large` 双按钮必须等分宽度，按钮之间使用 `spacing-12`。
- `vertical-large` 主行动按钮使用 Button `xlarge`，高度 `54px`。
- `vertical-compact` 的主标题或权益数值使用 `font-size-20` / `line-height-28`，不使用 AmountText。
- `vertical-compact` 的按钮宽度跟随小卡内容区自适应，不按文字宽度收缩。
- `vertical-compact` 2 列卡片按钮高度使用 `32px`。
- `vertical-compact` 3 列卡片按钮高度使用 `28px`。
- `vertical-compact` 的列间距固定使用 `spacing-8`。
- `horizontal-task` / `horizontal-product` 的右侧操作按钮统一使用 `small` 尺寸，固定为 `64px × 32px`。
- 左右布局的右侧按钮必须右对齐，距离 Card 右内边距 `spacing-card-padding-x`。
- 左右布局的右侧按钮不按文案自适应宽度，避免同一列表内按钮大小不一致。

## 7. 状态

```txt
default：默认展示。
disabled：不可点击或不可选择时使用。
```

规则：

- `interactive` 必须能被识别为可点击入口，例如右侧箭头、入口文案或明确的跳转语义。
- `disabled` 需要降低可交互感，但不能降低到不可读。

## 8. Token 使用

```txt
卡片背景：color-bg-card
卡片圆角：radius-card
卡片内边距：spacing-card-padding
卡片内部间距：spacing-list-gap
卡片之间间距：spacing-section-gap
卡片阴影：shadow-sm 或 shadow-none
卡片标题：color-text-primary / text-title-sm
卡片正文：color-text-secondary / text-body-md
卡片辅助文字：color-text-tertiary / text-body-sm
高亮内容：color-text-highlight
金额内容：text-amount-* / color-text-primary 或 color-text-highlight
卡片操作：Button
状态标签：Tag
```

## 9. 内容元素

```txt
icon:
  用途：卡片图标、任务图标、产品 logo、提示图标。
  位置：leading / header / body。

  task-icon:
    用途：任务、认证、待办、步骤、资料补充类条目中的 leading icon。
    container-size: 40px。
    icon-size: 24px。
    container-shape: circle。
    fallback: assets/icons/card-task-default.svg。

  product-logo:
    用途：产品、机构、品牌、方案类条目中的 leading logo。
    icon-size: 16px。
    container: none。
    fallback: 无对应 logo 时使用首字母 / 简化符号占位。

  notice-icon:
    用途：提示、状态、说明类图标。
    icon-size: 16px / 20px。

title:
  用途：卡片标题、任务名称、产品名称。
  样式：text-title-sm。
  字重：font-weight-semibold。
  颜色：color-text-primary。
  行数：最多 1 行。

subtitle:
  用途：副标题、说明文字、辅助信息。
  样式：text-body-sm。
  颜色：color-text-secondary 或 color-text-tertiary。
  行数：最多 2 行。

amount:
  用途：金额、额度、可借金额、可用金额、最高可借额度。
  样式：text-amount-md / text-amount-lg / text-amount-hero。
  字重：vertical-large 单列大卡使用 bold；其他卡片金额使用 medium。
  颜色：color-text-primary 或 color-text-highlight。

metric:
  用途：利率、折扣、期限、百分比、数量。
  样式：text-title-sm 或 text-body-md。
  字重：默认 medium。
  颜色：color-text-primary 或 color-text-highlight。

tag:
  用途：活动标签、状态标签、推荐标签。
  组件：Tag。

action:
  用途：卡片内主操作、跳转入口、状态操作。
  组件：Button。
```

规则：

- `icon` 只表达类别、状态或品牌，不承担主信息。
- `task-icon` 用于 `horizontal-task` 的 leading 区域。
- `product-logo` 用于 `horizontal-product` 的 leading 区域。
- 图标角色按内容语义和结构位置判断，不按业务标题精确命中。
- 无对应 `task-icon` 资源时，必须使用 `assets/icons/card-task-default.svg`。
- 无对应 `product-logo` 资源时，使用首字母 / 简化符号占位，不临时绘制品牌 logo。
- `title` 是卡片或条目的主识别信息。
- Card 内所有 `title` 元素默认使用 `text-title-sm`，不使用 `text-body-md`。
- `title` 必须使用加重字重，用于表达条目主识别信息。
- `subtitle` / `label` / `remark` 不加重，使用普通字重。
- `subtitle` 只放辅助说明，不放核心金额。
- 金额、额度、资产数字必须使用 `amount` 元素。
- 利率、折扣、期限等非金额数字使用 `metric`。
- 操作按钮统一使用 Button，不在 Card 内临时绘制按钮。
- Card 内最多一个主操作按钮。
- 不要新增 `vertical-title`、`horizontal-title` 这类布局专用元素。

## 10. 布局组合

```txt
vertical:
  header:
    title + extra / action
  body:
    amount / metric / content
  footer:
    action / remark

horizontal-task:
  leading:
    icon
  content:
    title
    subtitle: max-lines 1 / overflow ellipsis
  trailing:
    action

horizontal-product:
  product-row:
    product-logo + product-name + tag
  metric-row:
    amount-group + metric-group + action
  amount-group:
    amount
    amount-label
  metric-group:
    metric
    metric-label
  action:
    action

product-list:
  wrapper: Card
  item: horizontal-product
  item-gap: spacing-0
  item-separator: optional divider
  padding-top: spacing-card-padding-y
  padding-bottom: spacing-card-padding-y
```

规则：

- `vertical` 是默认组合，用于整张卡片内容上下排列。
- `horizontal-task` 用于任务行、认证项、资料补充项、待办事项。
- `horizontal-product` 用于产品项、机构额度、利率信息、推荐方案。
- `horizontal` 卡片右侧只放一个主操作，不放多个按钮。
- `horizontal-task` 的次标题仅展示 1 行，超出使用省略号，不允许换行撑高列表项。
- `horizontal-product` 的 product-logo、product-name、tag 必须同一行展示。
- `horizontal-product` 必须分为两层信息：第一层是产品识别信息，第二层是额度、利率和操作。
- `horizontal-product` 不允许把产品名、标签、金额、利率、按钮全部排在同一视觉行。
- `horizontal-product` 中金额和利率必须组成独立指标组，指标值在上、指标说明在下。
- 如果有多个 `horizontal-task` 项，外层使用 `task-list` Card，内部每一行使用 `horizontal-task`。
- 当 `horizontal-product` 数量大于 1 时，必须组合成 `product-list`，外层只使用一个 Card。
- `task-list` / `product-list` 内部列表项之间不使用大间距，列表项数量大于 1 时必须使用分割线区分。
- 分割线与上下列表项内容之间统一使用 `spacing-16`。
- `product-list` / `task-list` 的分割线分为三档：弱分割使用 `color-border-default` + `opacity-30`，中分割使用 `color-border-default` + `opacity-70`，强分割使用 `color-border-default` 且不叠加透明度。
- `task-list` / `product-list` 的外层 Card 必须保证上下 padding 一致，不允许出现顶部贴边或底部留白过大的情况。

## 11. 内容模式

```txt
summary:
  用于额度、金额、授信结果、账户概览等核心信息展示。
  常见结构：主数值 + 辅助说明 + 操作按钮。
  首页场景：额度主卡。

benefit:
  用于提额、免息、折扣、优惠券、权益包等权益信息。
  常见结构：权益数值 + 权益说明 + 操作按钮。
  首页场景：权益卡 / 活动卡。

task-list:
  用于认证任务、资料补充、步骤清单、待办事项。
  常见结构：标题 + 多个任务行，每一行使用 horizontal-task，不是独立 Card。
  首页场景：任务卡 / 任务列表卡。

product:
  用于产品列表、机构额度、利率信息、推荐方案。
  常见结构：产品名称 + 金额 / 利率 + 操作按钮。

notice:
  用于卡片内提示、说明、补充信息。
  常见结构：提示图标 / 标题 + 说明文字。
  title: max-lines 1
  subtitle: max-lines 1 / overflow ellipsis
```

规则：

- 内容模式用于指导卡片内部信息组织，不等于新增组件类型。
- 优先选择一个最贴近的内容模式，不要为每个业务词新增模式。
- `task-list` 的外层容器是 Card，内部每一行使用列表项结构。
- `benefit` 可配合 `highlight` 使用，但不强制等同于 `highlight`。
- `product` 可配合 `interactive` 使用，但不强制等同于 `interactive`。
- `notice` 用于轻量提示，不承载长说明；标题和说明默认单行展示。

## 12. 场景映射

```txt
普通信息分组 / 表单分组 / 详情信息 / 列表区块：
  type: default
  pattern: summary / task-list / notice

营销权益 / 优惠信息 / 重点提示 / 额度亮点：
  type: highlight
  pattern: benefit / summary

点击进入详情 / 选择项目 / 跳转入口 / 轻量操作入口：
  type: interactive
  pattern: product / benefit / summary

首页额度主卡：
  type: highlight
  pattern: summary
  layout: vertical-large
  content: 额度 / 可借金额 / 状态说明 / 卡片内主按钮
  title: 不外置页面区块标题，金额信息即主内容
  rule: 金额信息按垂直结构组织，主内容到按钮使用 spacing-32

首页任务卡 / 任务列表卡：
  type: default 或 interactive
  pattern: task-list
  layout: list-card + horizontal-task
  content: 任务标题 / 任务说明 / 去完成按钮

首页权益卡 / 活动卡：
  type: highlight 或 interactive
  pattern: benefit
  layout: vertical-compact 或 vertical
  content: 权益标题 / 权益说明 / 卡片内按钮
  section-title: 使用 PAGE_RULES.md 的 page-section-title，标题放在 Card 外部

首页产品推荐列表卡：
  type: default 或 interactive
  pattern: product-list
  layout: list-card + horizontal-product
  content: 产品名称 / 额度 / 利率 / 右侧操作按钮
  section-title: 使用 PAGE_RULES.md 的 page-section-title，标题放在 Card 外部
```

## 13. AI 生成流程

```txt
1. 判断内容是否属于同一主题。
   - 不是同一主题：拆成多个 Card 或改用页面分区。
   - 是同一主题：继续判断类型。

2. 判断 Card 类型。
   - 普通信息承载：default
   - 强调营销、权益、优惠、重点内容：highlight
   - 可点击、可选择、可进入详情：interactive

3. 判断内容模式。
   - 额度、金额、结果概览：summary
   - 提额、免息、折扣、优惠、权益：benefit
   - 认证任务、待办、步骤清单：task-list
   - 产品、机构、方案列表：product
   - 提示、说明、补充信息：notice

4. 判断内容元素。
   - 图标、logo、状态符号：icon
   - 主标题、任务名、产品名：title
   - 说明文字、辅助信息：subtitle
   - 金额、额度、授信金额：amount
   - 利率、折扣、期限、百分比：metric
   - 标签：tag
   - 操作按钮：action

5. 判断布局组合。
   - 上下信息组织：vertical
   - 任务行、认证项、待办事项：horizontal-task
   - 产品、机构、额度利率项：horizontal-product

6. 判断内容结构。
   - 有标题或右侧操作：使用 header
   - 有核心内容：使用 body
   - 有底部操作或备注：使用 footer

7. 套用布局与 Token。
   - 背景、圆角、间距、阴影、文字样式必须来自 Token。
```

## 14. 内容规则

- 卡片内只放同一主题下的信息。
- 卡片标题应简短明确。
- 卡片内主次信息需要有清晰层级。
- 可点击卡片必须有明确入口感。
- 禁用卡片需要降低可交互感。

## 15. AI 使用规则

- 相关内容应放在同一卡片中。
- 不要为了单纯增加间距而使用卡片。
- 重点营销内容、优惠信息可使用 `highlight`。
- 可点击卡片使用 `interactive`。
- 先判断 Card 类型，再判断内容模式。
- 先判断操作数量，再决定按钮组合；不要默认生成双按钮。
- Card 内金额必须调用 AmountText 规则，不使用普通标题样式代替。
- 元素 token 只按内容元素定义一次，不按布局重复定义。
- 内部间距按元素关系套用，不按业务卡片写死数值。
- 卡片内不允许出现临时颜色、临时圆角和临时间距。
- 不允许用多个嵌套卡片制造复杂层级。


## 17. 项目第一版启用范围

### 17.1 启用的内容模式
- 第一版启用全部标准内容模式：
  - `summary`
  - `benefit`
  - `task-list`
  - `product`
  - `notice`

### 17.2 启用的布局组合
- 第一版启用以下高频布局组合：
  - `vertical`
  - `vertical-large`
  - `vertical-compact`
  - `horizontal-task`
  - `horizontal-product`
  - `list-card`
  - `horizontal-row`

### 17.3 默认优先映射
- 金额、额度、可借金额、可用金额等核心数值信息：
  - 默认优先使用 `summary + vertical-large`
- 权益、优惠、活动、营销内容：
  - 默认优先使用 `benefit + vertical-compact`
- 待办、认证、补资料、步骤任务：
  - 默认优先使用 `task-list + list-card + horizontal-task`
- 产品推荐、借款方案、额度方案：
  - 默认优先使用 `product + list-card + horizontal-product`
- 普通说明、补充信息、提示信息：
  - 默认优先使用 `notice` 或 `default + vertical`

### 17.4 防误用规则
- 不要用 `vertical-large` 承载普通说明类内容
- 不要用 `vertical-compact` 承载长文信息内容
- 不要把 `horizontal-product` 用在任务列表场景
- `task-list` 可用于权益活动类内容，但前提是内容本质上属于多条任务、步骤或待完成项
- 同一区块允许混用多种卡片布局，但必须有明确的信息层级和分组理由

### 17.5 与页面规则的边界
- Card 内部结构、元素关系、按钮组合、金额样式以 Card 组件规范为准
- Card 外部与页面其他模块的间距、卡片在页面中的区块位置以页面布局规则和 page patterns 为准
- 若页面规则与 Card 内部布局冲突，优先遵守：
  - 页面规则决定区块层级和外部位置
  - Card 规则决定卡片内部组织方式


## 16. 禁止项

- 不要用 Card 代替页面间距。
- 不要把多个无关主题塞进同一个 Card。
- 不要把内容模式当成新的视觉类型。
- 不要把布局组合当成新的视觉类型。
- 不要在 Card 内嵌套 Card 制造复杂层级。
- 不要硬编码背景、圆角、间距、阴影或文字样式。
- 不要硬编码 Card 内部元素间距。
- 不要把金额、额度当成普通标题处理。
- 不要在未明确双操作时默认生成两个按钮。
- 不要让卡片内按钮按文案宽度过度收缩。
- 不要让不可点击 Card 表现得像可点击入口。
- 不要为 Card 增加未定义的按压态。
