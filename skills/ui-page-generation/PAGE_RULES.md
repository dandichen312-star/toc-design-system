# Page Rules 页面生成框架

## 1. 用途与边界

PAGE_RULES 是 H5 页面生成的唯一页面规则入口，用于定义页面级通用布局、页面类型 pattern、主按钮位置、设备展示层和 AI 页面生成顺序。

规则：

- PAGE_RULES 只定义页面骨架、页面级布局、页面级模块组合、页面类型 pattern 和页面读取顺序。
- 具体组件样式必须读取 `COMPONENT_RULES.md` 和对应组件文档。
- 页面框架不新增业务组件；首页额度主卡、任务卡、权益卡、活动卡归入 `Card.md` 场景。
- `全局页面布局规则.md` 和 `page-patterns.md` 的有效规则已合并到本文档，AI 生成页面时不再以旧文件作为入口。

## 2. 页面类型

```txt
home-page:
  用途：首页、借款首页、任务型首页。
  当前状态：详细定义。

form-flow-page:
  用途：资料填写、实名认证、银行卡绑定、补充资料。
  当前状态：详细定义。

list-page:
  用途：消息列表、交易记录、账单列表、任务列表。
  当前状态：基础 pattern。

detail-page:
  用途：借款详情、账单详情、还款详情。
  当前状态：基础 pattern。

result-page:
  用途：申请成功、申请失败、审核中、操作成功、空状态。
  当前状态：基础 pattern。

agreement-page:
  用途：借款协议、会员协议、风险提示、产品说明。
  当前状态：基础 pattern。

account-asset-page:
  用途：可用额度、账户信息、权益信息、任务入口。
  当前状态：基础 pattern。

marketing-page:
  用途：优惠、权益、活动承接、转化落地页。
  当前状态：reserved。
```

## 3. 全局页面结构

```txt
Page
├── background-layer 可选
├── page-header 必填
├── content-layer 必填
│   ├── global-notice 可选
│   └── section / card / form / list
└── action-footer 可选
```

规则：

- 设计基准尺寸为 `375px * 812px`。
- 页面宽度自适应，开发按项目单位换算规则适配，不按固定像素写死页面宽度。
- 页面默认背景使用 `color-bg-page`。
- 卡片、表单卡片、模块容器默认背景使用 `color-bg-card`。
- 页面内容层左右边距使用 `spacing-16`。
- 页面级模块间距使用 `spacing-12`。
- 页面内容默认从标题栏下方开始，标题栏底部到正文内容顶部固定 `spacing-16`。
- 非首页页面中，首个内容模块距离标题栏底部固定 `spacing-16`。
- 背景层可以铺满屏幕宽度，不受页面左右边距限制。
- 内容层和组件模块必须遵守页面左右边距。
- 页面默认采用纵向滚动。
- 标题栏固定在页面顶部。
- 底部固定操作区如存在，固定在页面底部。

页面区块标题：

```txt
page-section-title:
  position: above-card
  align: left
  text-style: text-section-title
  font-size: 16px
  line-height: 24px
  gap-to-card: spacing-8
```

规则：

- 页面区块标题用于福利权益、产品推荐等页面模块标题。
- 页面区块标题放在 Card 外部、Card 上方，不参与 Card 内部结构。
- 页面区块标题与对应 Card 之间固定使用 `spacing-8`。
- Card 内部不重复展示同名标题，避免页面标题和卡片标题重复。

## 4. 设备展示层

设备展示层用于 Figma 页面还原，表达手机状态栏、首页底部菜单栏和底部安全区。它们属于设备 / 宿主区域，不是业务组件。

```txt
figma-render-shell:
  required: true
  frame-size: 375px * 812px

status-bar:
  required: true
  height: 44px
  position: top

home-indicator:
  required: true
  height: 34px
  position: bottom

bottom-tab-bar:
  applies-to: home-page
  required: true
  height: 56px
  position: above home-indicator
  item-count: 2-5
  default-item-count: 2
```

规则：

- Figma 生成完整页面时，必须绘制 `status-bar`、`page-header`、`content-layer` 和 `home-indicator`。
- Figma 生成首页时，必须额外绘制 `bottom-tab-bar`。
- 除非用户明确要求“只生成业务内容区域”，否则不允许省略设备展示层。
- `status-bar` 和 `home-indicator` 只用于 Figma 展示，真实前端实现可由系统或宿主容器处理。
- `status-bar` 不计入 `page-header` 高度，`page-header` 仍为 `44px`。
- `status-bar` 的底色应跟随 `page-header` 当前底色变化；首页透明态时保持透明，吸顶白底时同步为白底。
- 首页内容区底部必须停在 `bottom-tab-bar` 上方，不能被底部菜单栏遮挡。
- 表单流程页不展示 `bottom-tab-bar`，使用 `action-footer` 和 `home-indicator`。
- 首页不使用全局 `action-footer`。
- `home-indicator` 所在底色必须跟随底部吸附元素变化；首页底部菜单栏存在时与 `bottom-tab-bar` 保持一致，页面存在 `action-footer` 时与 `action-footer` 保持一致。
- 当页面底部不存在 `bottom-tab-bar`、`action-footer` 或其他底部吸附容器时，`home-indicator` 独立存在，背景必须为透明。

## 5. 页面标题栏

```txt
global-page-header:
  height: 44px
  padding-x: spacing-16
  title:
    font-size: font-size-16
    line-height: line-height-24
    font-weight: font-weight-medium
```

首页标题栏：

```txt
home-header:
  height: 44px
  title-align: left
  back-button: none
  right-action: message icon
  initial-background: transparent
  initial-foreground: auto-contrast
  scrolled-background: color-bg-card
  scrolled-foreground: default
```

流程页 / 内页标题栏：

```txt
flow-header:
  height: 44px
  title-align: center
  back-button: left
  right-action: optional
  background: color-bg-card
```

规则：

- 首页以外的页面默认必须有标题栏。
- 标题栏高度固定为 `44px`。
- 标题栏左右内边距固定使用 `spacing-16`。
- 标题栏标题使用 `Header.md` 的 `header-title` 规则：`font-size-16`、`line-height-24`、`font-weight-medium`。
- 标题栏紧贴状态栏，不额外增加顶部间距。
- 标题文案建议控制在 `8` 个字符内。
- 标题栏默认不带底部分割线和阴影。
- 首页标题栏左侧展示页面标题，不展示返回按钮。
- 首页标题栏右侧默认展示消息图标，图标引用 `Icon.md` 的 `message`。
- 首页标题栏初始背景透明，页面下滑后标题栏背景反白为 `color-bg-card`。
- 首页标题栏初始透明时，标题和右侧图标必须遵守 `COMPONENT_RULES.md` 的全局前景对比规则；深色背景上使用反白文字和反白图标。
- 首页标题栏下滑反白后，标题和图标恢复默认前景色。
- 内页标题栏左侧默认展示返回按钮，图标引用 `Icon.md` 的 `back`。
- 内页标题栏标题默认居中，标题栏背景默认 `color-bg-card`。
- 页面正文内容不能被标题栏遮挡。

## 6. 背景层

```txt
page-background:
  default: color-bg-page

background-layer:
  allowed-pages: home-page / result-page / marketing-page
  fill: solid / gradient / image
  height: viewport-height * 44%
  position: top
  width: 100%
  z-index: behind content
  fade-mask: required
  fade-to: color-bg-page
```

规则：

- 首页、结果页、营销页允许使用顶部背景层。
- 背景层默认高度为屏幕高度的 `44%`，在 `375px * 812px` 设计基准下约为 `360px`。
- 背景层可以填充纯色、渐变、背景图或装饰图形。
- 背景层必须遵守 `COMPONENT_RULES.md` 的全局背景层渐隐规则：从背景层高度 `70%` 开始，到 `100%` 融合到 `color-bg-page`。
- 背景层不参与内容 Auto Layout / Flex。
- 首页背景层可以铺到标题栏背后。
- 首页正文内容仍从标题栏下方 `spacing-16` 开始。
- 表单流程页默认不使用强背景层，除非业务明确要求。

页面类型默认背景映射：

```txt
home-page:
  background-fill: gradient-surface-brand-strong

result-page:
  background-fill: gradient-surface-brand-soft

review-waiting-page:
  background-fill: gradient-surface-brand-soft

review-result-page:
  background-fill: gradient-surface-brand-soft

marketing-page-blue:
  background-fill: gradient-surface-brand-strong

marketing-page-orange:
  background-fill: gradient-surface-warm
```

- `review-waiting-page` / `review-result-page` / `result-page` 禁止使用 `gradient-surface-brand-strong`。
- 切换 `brand theme` 只允许替换同档位主题色，不允许将上述页面背景提升为更强档位。

用户提供背景图规则：

- 用户提供 png / jpg / webp 时，将图片填入当前页面类型的 `background-layer`。
- 背景图高度跟随 `background-layer` 容器高度，不单独决定页面背景高度。
- 背景图使用 `cover` 填满背景层，默认 `top center` 对齐。
- 背景图也必须应用背景层底部渐隐，最终融合到 `color-bg-page`。

## 7. 底部固定操作区

```txt
action-footer:
  applies-to: form-flow-page / detail-page / agreement-page
  default-button: Button.md primary + large + full
  position: fixed-bottom
  z-index: above content-layer
  device-layer: home-indicator above action-footer
  content-avoid: required
```

规则：

- 固定底部操作区位于页面内容之上，正文内容必须避让 `action-footer`。
- `home-indicator` / 底部系统 bar 属于设备展示层，层级高于所有页面内容和 `action-footer`。
- `action-footer` 背景可以铺到底部设备区域下方，但按钮不能被 `home-indicator` 遮挡。
- 按钮底部间距只保留按钮到可视安全边界的必要距离，不因为 `home-indicator` 再额外叠加大留白。
- 固定底部操作区默认以单按钮布局为主，同时兼容双按钮布局。
- 正文内容必须避让底部操作区，不得被按钮区域遮挡。
- 表单流程页默认使用 `action-footer`。
- 详情页、协议与说明页可按业务使用 `action-footer`。
- 结果页主按钮默认放在内容区内，不固定到底部操作区。
- 首页不默认使用 `action-footer`；首页按钮必须跟随模块。

## 8. Notice 位置

```txt
global-notice:
  position: content-start
  below-page-header-gap: spacing-0
  top-gap: spacing-0
  width: page-width
  ignore-content-padding-x: true
  component: Notice.md

local-notice:
  position: inside-module
  component: Notice.md
```

规则：

- 页面级 Notice 放在正文内容第一项，但不按普通业务模块处理。
- 页面级 Notice 紧跟 `page-header` 时，标题栏底部到 Notice 顶部的间距固定为 `spacing-0`。
- 页面级 Notice 不继承 `content-layer` 的左右 `spacing-16`，默认宽度跟随页面宽度。
- 页面级 Notice 位于内容区顶部时，顶部间距固定为 `spacing-0`。
- 页面级 Notice 自身内部 padding、图标、文字和滚动行为由 `Notice.md` 决定。
- 页面级 Notice 下方到第一个业务模块使用页面模块间距 `spacing-12`。
- 局部 Notice 放在对应模块或 Card 内部。
- Notice 不吸顶、不悬浮，除非页面明确声明。
- 局部 Notice 与同模块内其他内容的间距按所属组件文档决定。

## 9. 卡片、空状态与异常状态

卡片容器规则：

- 卡片默认占满内容区宽度。
- 卡片内部内边距、描边、圆角和内部结构由 `Card.md` 定义。
- 页面只决定 Card 所在区块、外部间距和模块组合，不定义 Card 内部样式。

空状态规则：

- 空状态默认包含图标和标题。
- 空状态说明文案为可选。
- 空状态按钮为可选。
- 空状态内容默认在内容区内垂直居中。
- 空状态页面允许保留顶部标题栏。
- 空状态下如有按钮，默认放在空状态内容块内部。

加载与异常状态规则：

- 加载中默认优先使用局部 skeleton。
- 错误状态和无网络状态默认与空状态共用同一套布局骨架。
- 错误状态和无网络状态默认提供重试按钮。
- 加载、错误、无网络等状态页面允许保留顶部标题栏。

## 10. 首页框架

首页分为借款首页和任务型首页。

```txt
loan-home-page:
  device-shell: status-bar + home-indicator
  page-header: home-header
  background-layer: optional
  content-layer:
    hero-amount-card
    global-notice optional
    task-card optional
    benefit-card / activity-card optional
    product-list-card optional
  bottom-tab-bar: required

task-home-page:
  device-shell: status-bar + home-indicator
  page-header: home-header
  background-layer: optional
  content-layer:
    status-card
    global-notice optional
    task-list-card
  bottom-tab-bar: required
```

规则：

- 首页不默认使用 `action-footer`。
- 首页默认展示 `bottom-tab-bar`。
- 首页按钮必须跟随模块，例如额度主卡、任务卡、活动卡内部按钮。
- 借款首页必须有首页额度主卡。
- 任务型首页必须有状态卡和任务列表卡。
- 首页中的额度主卡、任务卡、任务列表卡、权益卡、活动卡、产品推荐列表卡都使用 `Card.md` 的场景规则。
- 首页模块之间使用 `spacing-12`。
- 首页金额大卡默认位于标题栏下方的第一个业务区块。
- 首页允许出现功能入口区、推荐产品区、活动区和多个营销模块。
- 首页不允许默认生成固定底部操作区；只有业务明确要求时才允许升级。

## 11. 表单流程页框架

```txt
basic-form-flow-page:
  device-shell: status-bar + home-indicator
  page-header: flow-header
  content-layer:
    global-notice optional
    FormCard
  action-footer: required

complex-form-flow-page:
  device-shell: status-bar + home-indicator
  page-header: flow-header
  content-layer:
    global-notice optional
    FormCard / FormSection multiple
  action-footer: required
```

规则：

- 基础表单默认结构为 `Notice 可选 + 单个 FormCard + action-footer`。
- 复杂表单允许多个 `FormCard / FormSection`。
- 表单流程页必须使用全局 `action-footer` 规则。
- 表单内容区使用滚动或填充布局，不允许被底部按钮遮挡。
- 表单默认采用单列纵向排列。
- 说明提示区和协议区按需出现。
- 键盘弹起时，底部按钮区需要保持可见。
- 表单项遵守 `Form.md`、`FormItem.md`、`Input.md`、`PickerSheet.md`。
- `picker-row` 点击后使用 `PickerSheet.md`。

## 12. 列表页框架

```txt
list-page:
  device-shell: status-bar + home-indicator
  page-header: flow-header
  content-layer:
    list-section
    empty-state optional
  action-footer: optional
```

规则：

- 列表页适用于消息列表、交易记录、账单列表、任务列表。
- 列表页第一版默认不配置筛选区。
- 列表内容排列方式按具体组件规范决定，默认优先单列。
- 列表项默认占满内容区宽度。
- 主按钮如有出现，默认跟随内容展示，不默认固定到底部。
- 列表为空时使用空状态规则。

## 13. 详情页框架

```txt
detail-page:
  device-shell: status-bar + home-indicator
  page-header: flow-header
  content-layer:
    amount-section optional
    info-card-section
    notice / risk-tip optional
    marketing-section optional
  action-footer: optional
```

规则：

- 详情页适用于借款详情、账单详情、还款详情。
- 详情页顶部可包含金额区。
- 信息卡片区默认采用多组卡片分区展示。
- 说明文案和风险提示按需出现。
- 详情页允许插入营销模块。
- 详情页存在强主按钮时，可使用 `action-footer`。

## 14. 结果页框架

```txt
result-page:
  device-shell: status-bar + home-indicator
  page-header: flow-header
  background-layer: optional
  content-layer:
    status-icon-section
    title-section
    description-section optional
    action-section
      button: Button.md primary + large + full
    task-card / product-card optional
  action-footer: none by default
```

规则：

- 结果页适用于申请成功、申请失败、审核中、操作成功、空状态。
- 结果页主内容默认采用偏上布局。
- 按钮区默认使用单主按钮，放在内容区内。
- 结果页内容区主按钮属于页面主 CTA，必须使用 `Button.md primary + large + full`。
- 结果页内容区主按钮宽度跟随页面内容区可用宽度，在 `375px` 基准下为 `375 - spacing-16 * 2 = 343px`。
- 结果页内容区主按钮不得临时使用固定窄宽或额外容器制造左右留白。
- 结果页主按钮默认不固定到底部操作区。
- 审核中页面沿用结果页基础 pattern。
- 结果页允许增加任务卡片、推荐产品和后续引导模块。
- 审核等待页、审核结果页默认可使用 `gradient-surface-brand-soft` 背景层。
- `result-page` / `review-waiting-page` / `review-result-page` 在任意 `brand theme` 下都必须保持 soft 档位，不得升级到 `gradient-surface-brand-strong`。

## 15. 协议与说明页框架

```txt
agreement-page:
  device-shell: status-bar + home-indicator
  page-header: flow-header
  content-layer:
    content-section
    confirm-check optional
  action-footer: optional / required by business
```

规则：

- 协议与说明页适用于借款协议、会员协议、风险提示、产品说明。
- 正文默认采用标题加正文块结构。
- 勾选确认区按需出现。
- 风险提示页与协议页共用同一套基础 pattern。
- 正文中默认不插入强调卡片或提示框。
- 协议 / 说明页正文内容默认左右边距可提升为 `24px`。
- 如页面需要确认继续，默认使用 `action-footer`。

## 16. 账户与资产页框架

```txt
account-asset-page:
  device-shell: status-bar + home-indicator
  page-header: flow-header
  content-layer:
    amount-section
    list-group-section
    benefit-section optional
    marketing-section optional
  action-footer: optional
```

规则：

- 账户与资产页适用于可用额度、账户信息、权益信息、任务入口。
- 顶部默认包含核心金额信息区。
- 页面内容默认采用列表分组。
- 允许营销位或权益位插入主内容流中。
- 默认不设置固定底部操作区；如具体业务页存在强主按钮，可按业务升级为固定底部操作区。
- 账户与资产页默认以信息聚合和入口分发为主。

## 17. 营销页框架

```txt
marketing-page:
  device-shell: status-bar + home-indicator
  page-header: optional / flow-header
  background-layer: allowed
  action-footer: optional
```

规则：

- 当前阶段不详细定义营销转化页。
- 营销页允许背景层，默认高度同背景层规则。
- 营销页是否使用底部按钮由具体页面决定。
- 营销页背景可使用蓝色或橙色主题：`gradient-surface-brand-strong` / `gradient-surface-warm`。

## 18. 页面生成读取与执行优先级

```txt
1. DESIGN_TOKENS.md
   决定所有原子值来源：颜色、字号、间距、圆角、阴影、数字字体等。

2. PAGE_RULES.md
   决定页面类型、页面骨架、模块顺序、页面级留白、模块间距、组件所在区块、组件外部位置和组件可用宽度。

3. COMPONENT_RULES.md
   决定全局组件约束、组件选择原则、前景对比、背景渐隐、数字字体、禁止临时样式。

4. 具体组件文档
   例如 Header.md / Card.md / Button.md / Icon.md。
   按当前页面实际使用到的组件按需读取。
   决定组件内部结构、内部间距、字号、按钮规格、图标尺寸和组件内部布局。
```

页面生成流程：

```txt
1. 读取 DESIGN_TOKENS.md，建立 token 来源。
2. 读取 PAGE_RULES.md，判断页面类型和页面 pattern。
3. 根据页面类型确定页面骨架、设备展示层、背景层、标题栏、模块顺序和页面级间距。
4. 读取 COMPONENT_RULES.md，确认全局组件约束和组件选择原则。
5. 根据当前页面实际用到的组件，读取对应组件文档。
6. 放置组件实例，并将页面内容区宽度传递给组件。
7. 组件内部结构、字号、间距、按钮规格和图标尺寸由组件文档自适应决定。
```

冲突处理：

- 页面规则决定组件放在哪里、占多宽、与上下模块间距多少。
- 组件规则决定组件内部怎么排。
- `DESIGN_TOKENS.md` 决定所有具体数值来源。
- 页面规则不能重写组件内部结构。
- 组件规则不能改写页面模块顺序。
- 不允许因为页面宽度变化，临时放大组件内部字号、按钮、图标或间距。
- AI 不得混淆首页、结果页、协议页和表单页的主按钮位置。
- 若页面需求不完全命中某个 pattern，应优先复用最接近的 pattern，再做最小调整。

## 19. 禁止项

- 不要把首页主按钮默认画成吸底按钮。
- Figma 完整页面生成时，不要省略 status-bar、home-indicator 或首页 bottom-tab-bar。
- 不要让正文内容被标题栏遮挡。
- 不要让首页正文被 bottom-tab-bar 遮挡。
- 不要让正文内容被 action-footer 遮挡。
- 不要在页面框架中临时创造组件样式。
- 不要把背景层放进内容 Auto Layout 中。
- 不要为首页额度主卡、任务卡、权益卡新增独立组件文档。
- 不要在表单流程页把提交按钮混入正文内容流。
- 不要在页面生成时重新绘制组件内部结构。
- 不要用页面规则覆盖 Card、Button、Icon、Input、Form 等组件文档中的内部规则。
- 不要同时读取旧页面规则后覆盖本文档中的最新约定。
