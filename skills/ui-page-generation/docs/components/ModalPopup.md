# Modal / Popup 弹窗

## 1. 用途

Modal / Popup 用于需要打断当前流程的场景，例如重要确认、风险提示、授权说明、营销提示、信息填写、底部选择和更多操作。

Modal / Popup 表达流程决策或阻断信息，不用于普通内容分组；普通信息分组应使用 Card。

## 2. 类型

```txt
alert：纯提示、告知、规则说明。
confirm：需要用户明确确认或二选一决策。
form：弹窗内填写或补充信息。
marketing：营销权益、活动提示、福利确认、退出挽留。
bottom-sheet：底部弹层，用于选择项、协议说明、更多操作、退出挽留、营销权益。
```

AI 选择规则：

- 只需要用户知道结果或说明：使用 `alert`。
- 涉及风险、授权、扣费、删除、离开流程等决策：使用 `confirm`。
- 弹窗内需要填写内容：使用 `form`。
- 权益、活动、优惠、营销转化：使用 `marketing`。
- 从底部出现的选择列表、协议、更多操作：使用 `bottom-sheet`。

## 3. 内容结构

```txt
Modal:
  overlay 必填

  container 必填
    close 可选

    header 可选
      title 必填

    body 必填
      description / content

    footer 必填
      action

BottomSheet:
  overlay 必填

  sheet 必填
    handle 可选
    header 可选
    body 必填
    footer 可选
```

规则：

- `overlay` 用于遮罩页面，必须存在。
- `container` / `sheet` 承载弹窗内容，必须存在。
- `header` 只放标题，不放正文。
- 有 `header` 时，标题默认居中。
- `body` 承载正文、说明、表单、列表或权益内容。
- `footer` 只放操作按钮或次级操作，不承载主内容。
- `footer` 遵守 `COMPONENT_RULES.md` 的 `action-footer` 吸底规则。
- `close` 只在明确允许关闭、跳过或稍后处理时出现。
- 当 `footer.action = single-action` 且主按钮不是关闭确认语义时，默认显示 `close`。
- 当 `footer.action = single-action` 且主按钮文案为「我知道了」或「好的」时，必须隐藏 `close`。
- 「我知道了」和「好的」已表达关闭确认语义，不再额外显示右上角关闭按钮。
- 弹窗必须有明确主操作或明确关闭方式。
- 点击遮罩默认不关闭弹窗；只有页面明确声明允许点击遮罩关闭时，才可以覆盖此规则。

## 4. 尺寸与布局

```txt
modal:
  width: 300px
  max-height: 540px
  radius: radius-modal
  padding-x: spacing-24
  padding-y: spacing-24

marketing-modal:
  width: 300px
  height: 330px
  radius: radius-modal
  padding-x: spacing-24
  padding-y: spacing-24

bottom-sheet:
  width: fill / 100%
  max-height: 640px
  radius: radius-sheet top-left / top-right
  header-height: 60px
  padding-left: spacing-24
  padding-right: spacing-24
  padding-top: spacing-24
  padding-bottom: safe-area-bottom

overlay:
  width: viewport
  height: viewport
  z-index: z-index-overlay

container-layer:
  z-index: z-index-modal
```

规则：

- Modal / Popup 遵守 `COMPONENT_RULES.md` 的全局布局规则。
- 居中 Modal 默认宽度为 `300px`。
- 营销类中部弹窗固定宽度为 `300px`，固定高度为 `330px`。
- 超长内容时，Modal 最大高度为 `540px`，超过后 `body` 内部滚动。
- 营销内容不得撑高容器；内容超过 `330px` 时，优先精简权益信息，必须保留时仅 `body` 内部滚动。
- 超长内容滚动时，`header` 和 `footer` 必须保持可见。
- BottomSheet 宽度默认 `fill / 100%`，最大高度固定为当前设计稿基准值 `640px`。
- BottomSheet 默认使用内容自适应高度（`hug-content`），不允许无明确业务原因直接使用接近满屏的固定高度。
- 有 `header` 的 BottomSheet，标题区固定高度使用当前设计稿基准值 `60px`。
- BottomSheet 内容过长时，`body` 内部滚动。
- 只有当业务明确要求长内容承载、沉浸式阅读或大体量选择列表时，BottomSheet 才允许提升到更大的弹层高度；此时仍应优先使用 `max-height + body scroll`，不优先写死固定高。
- BottomSheet 左、右、上内边距使用 `spacing-24`。
- BottomSheet 底部内边距使用 `safe-area-bottom`，不额外叠加 `spacing-24`。
- 当 BottomSheet 没有 `footer` 时，正文内容区必须停在底部安全区之上。
- 当 BottomSheet 没有 `footer` 时，正文内容区左、右内边距固定使用 `spacing-32`。
- 无 `footer` 的 BottomSheet，正文内容区宽度跟随弹层可用宽度自适应，不允许额外缩成固定窄内容区。
- 无 `footer` 的 BottomSheet，正文内容区到底部安全区上边界固定使用 `spacing-40`。
- 因此无 `footer` 的 BottomSheet，正文内容区底部总留白 = `spacing-40 + safe-area-bottom`。

## 5. 内部间距

```txt
section-gap:
  header-body: spacing-16
  body-footer: spacing-24

item-gap:
  title-description: spacing-8
  paragraph-paragraph: spacing-8
  form-item-item: spacing-form-gap

marketing-gap:
  center-title-body: auto-even
  bottom-title-body: spacing-32
  amount-title-amount: spacing-4
  amount-amount-meta: spacing-8
  center-content-action: auto-even
  bottom-content-action: spacing-40

close:
  top: spacing-8
  right: spacing-8
```

布局规则：

```txt
default:
  header / body / footer 之间使用 section-gap
  标题与正文之间使用 title-description

long-content:
  body: scroll
  footer: fixed in container

with-close:
  close: absolute / overlay
```

规则：

- 弹窗内部间距按区域关系定义，不按业务场景写死。
- 标题与正文之间使用 `spacing-8`。
- 正文段落之间使用 `spacing-8`。
- 正文与按钮区之间使用 `spacing-24`。
- 中部固定高度营销弹窗使用三段式自适应布局：header 吸顶、footer 吸底、body 在 header 与 footer 之间的剩余空间内垂直居中。
- 中部固定高度营销弹窗不单独定义标题到主体内容、主体内容到按钮的固定间距，避免与固定高度、按钮高度产生冲突。
- 底部营销弹窗标题到主体内容使用 `spacing-32`。
- 金额标题到金额使用固定间距 `spacing-4`。
- 金额到辅助说明使用 `spacing-8`。
- 底部营销弹窗主体内容到按钮使用 `spacing-40`。
- 关闭按钮悬浮在容器右上角，不参与正文与按钮区的流式布局。
- 关闭按钮层级必须高于标题和正文。
- 带 `header` 的 BottomSheet 中，关闭按钮固定在标题区右上角，标题保持居中。

## 6. 操作按钮规则

```txt
single-action:
  使用 Button.md 的「单主按钮」

double-action:
  使用 Button.md 的「双按钮」

stacked-action:
  使用 Button.md 的「主按钮 + 次文本」
```

规则：

- 单按钮用于告知、确认、完成等单一主操作。
- 双按钮用于明确二选一决策，弱动作在左，强动作在右。
- 上下按钮用于主次差异很强的场景，上方主按钮，下方次文本。
- 不允许出现两个同视觉强度的主按钮。
- 涉及放弃、离开、取消权益等动作时，优先使用次文本或 danger text，不与主按钮同权。
- 弹窗内除 `text` 按钮外，所有按钮高度固定为 `48px`。
- 弹窗只判断使用哪种按钮组合，按钮尺寸、间距、颜色、字重和次文本规格均遵守 Button.md。
- 按钮规格必须复用 Button 组件规则，不在弹窗内临时绘制按钮。
- 单主按钮文案为「我知道了」或「好的」时，该按钮表示关闭确认，不与右上角 `close` 同时出现。

## 7. 状态

```txt
default：默认展示。
loading：主操作处理中。
disabled：按钮或表单不可操作。
scrollable：正文超长，需要内部滚动。
```

规则：

- `loading` 状态必须锁定重复提交。
- `disabled` 状态只作用于不可点击按钮或不可编辑表单项。
- `scrollable` 只作用于正文内容区，不让整个弹窗离开视口。

## 8. Token 使用

```txt
遮罩背景：color-bg-mask
弹窗背景：color-bg-elevated
弹窗圆角：radius-modal
底部弹层圆角：radius-sheet
弹窗阴影：shadow-lg
标题文字：color-text-primary / text-title-md
正文文字：color-text-secondary / text-body-md
辅助文字：color-text-tertiary / text-body-sm
高亮文字：color-text-highlight
边框或分割线：color-border-default
遮罩层级：z-index-overlay
弹窗层级：z-index-modal
弹窗按钮组合：Button.md
```

规则：

- 所有颜色、圆角、阴影、层级和文字样式必须来自 `DESIGN_TOKENS.md`。
- 弹窗按钮必须来自 Button 组件，并遵守 Button.md 的弹窗按钮组合规则。
- 不允许使用未在当前 `DESIGN_TOKENS.md` 中定义的旧项目 token 或旧文本样式名。

## 9. 内容元素

```txt
overlay:
  用途：阻断底层页面操作。
  样式：color-bg-mask。

container:
  用途：承载弹窗内容。
  样式：color-bg-elevated / radius-modal / shadow-lg。

sheet:
  用途：承载底部弹层内容。
  样式：color-bg-elevated / radius-sheet / shadow-lg。

title:
  用途：弹窗结论、操作目的、风险标题。
  样式：text-title-md。
  颜色：color-text-primary。
  行数：最多 1 行。

marketing-title:
  用途：营销弹窗主标题。
  默认样式：text-title-md。
  hero样式：text-title-lg。
  宽度：fill。
  行数：default 最多 2 行；hero 仅 1 行。

description:
  用途：说明原因、影响、规则、下一步。
  样式：text-body-md。
  颜色：color-text-secondary。

highlight:
  用途：突出金额、期限、权益、风险关键词。
  颜色：color-text-highlight。

benefit:
  用途：权益、优惠、会员福利、活动卖点。
  规则：颜色、圆角、文字必须来自 Token。

amount:
  用途：额度、可借金额、优惠金额、折扣数字。
  组件：AmountText。
  样式：text-amount-hero / text-amount-lg / text-amount-md。
  颜色：color-text-highlight 或 color-text-primary。

amount-title:
  用途：金额上方说明，例如“小标题(元)”。
  样式：text-body-md。
  颜色：color-text-secondary。

amount-group:
  用途：承载 amount-title / amount / amount-meta。
  宽度：fill。
  对齐：center / left。
  间距：amount-title 到 amount 使用 spacing-4；amount 到 amount-meta 使用 spacing-8。

marketing-content-panel:
  用途：承载 marketing 弹窗中的垂直核心内容组。
  使用条件：content-group.layout = vertical 且 content-group.align = center。
  不使用：content-group.align = left 或 content-group.layout = horizontal。
  背景：color-bg-card。
  圆角：radius-8。
  边框：none。
  padding-x: spacing-16。
  padding-y: spacing-16。

amount-meta:
  用途：金额下方辅助说明，例如有效期、失效时间、补充提示。
  样式：text-body-sm。
  颜色：color-text-tertiary。

coupon:
  用途：免息券、折扣券、息费优惠。
  结构：优惠数字 + 优惠名称。
  数字：AmountText medium / large。

marketing-background:
  用途：营销弹窗顶部背景氛围。
  渐变：gradient-surface-warm / gradient-surface-brand-soft / gradient-surface-brand-strong。
  规则：遵守 `COMPONENT_RULES.md` 的全局背景层规则和全局前景文本对比规则。
  位置：container 左上角。
  宽度：container width。

close:
  用途：允许关闭或稍后处理。
  位置：container 右上角。
  点击区域：24px。
  图标尺寸：12px。
  图标：assets/icons/icon-close.svg。
  颜色：color-icon-tertiary。

action:
  用途：确认、取消、提交、继续、返回等操作。
  组件：Button。
```

规则：

- `title` 必须短，优先单行展示。
- 默认营销标题使用 `text-title-md`，最多 2 行。
- 短营销标题可使用 `text-title-lg` 作为 hero 标题等级。
- `text-title-lg` 仅用于不超过 8 个中文字符的短营销结论，且必须单行展示。
- 超过 8 个中文字符，或包含较长数字 / 英文 / 折扣信息时，使用 `text-title-md`。
- 不允许根据实际文案长度临时创造新字号。
- `description` 小于 3 行时可居中；大于等于 3 行时左对齐。
- 超长正文必须左对齐。
- `highlight` 只用于正文中的关键短语，不用于整段正文。
- 营销弹窗中的金额、额度、折扣数字必须使用 AmountText。
- `hero` / `large` / `medium` 金额不与 `¥` / `￥` 组合。
- `amount-title`、`amount`、`amount-meta` 必须放在同一个 `amount-group` 内。
- `amount-group` 为居中时，`amount-title`、`amount`、`amount-meta` 全部居中；为居左时，三者全部居左。
- 不允许 `amount-title` 与 `amount` 使用不同对齐方式。
- `marketing-content-panel` 仅由 `content-group.layout` 和 `content-group.align` 决定，不由中部弹窗 / 底部弹窗决定。
- `content-group.layout = vertical` 且 `content-group.align = center` 时使用 `marketing-content-panel`。
- `content-group.align = left` 或 `content-group.layout = horizontal` 时不使用 `marketing-content-panel`。
- `marketing-content-panel` 不按金额、额度、折扣、权益类型拆分。
- 优惠券、折扣券、会员权益属于 `benefit` 内容，不新增弹窗类型。
- `marketing-background` 只作为背景层，不承载内容。
- 营销文案覆盖在 `marketing-background` 上时，文本颜色必须根据文字所在区域的实际背景色自动切换。
- 关闭按钮不替代主操作。

## 10. 布局组合

```txt
alert:
  header:
    title 可选
  body:
    description
  footer:
    single-action

confirm:
  header:
    title
  body:
    description
  footer:
    double-action / stacked-action

form:
  header:
    title
  body:
    form-content
  footer:
    single-action

marketing:
  background:
    marketing-background 可选
  header:
    title
  body:
    pattern: marketing-amount / marketing-coupon / marketing-benefit
  footer:
    single-action / stacked-action

bottom-sheet:
  header:
    title 可选
  body:
    list / content / form
  footer:
    action 可选
```

规则：

- `alert` 不承载复杂决策。
- `confirm` 必须明确主次动作。
- `form` 的输入项遵守 Form / Input 组件规则。
- `marketing` 可使用高亮文案，但必须来自 token。
- `marketing` 的渐变背景必须使用 `gradient-surface-*` token，并遵守 `COMPONENT_RULES.md` 的全局背景层规则。
- `placement = center / bottom` 只决定弹窗位置，不决定内容结构。
- 中部弹窗和底部弹窗使用相同的内容元素、间距、金额组和按钮规则。
- `alignment = left` 时，仅使用浅色背景，不使用深色或高饱和背景。
- `alignment = center` 时，可使用 `gradient-surface-*` 背景。
- `bottom-sheet` 适合选择项、说明信息或轻量操作，不用于强决策确认。

## 11. 内容模式

```txt
marketing-amount:
  amount-title 可选
  amount: AmountText hero / large
  amount-meta 可选

marketing-coupon:
  coupon-title 可选
  coupon-value: AmountText medium / large
  coupon-desc 可选

marketing-benefit:
  benefit-title
  benefit-desc 可选
  highlight 可选
```

规则：

- `marketing-amount` 用于额度通过、可借额度、核审通过等金额转化场景。
- `marketing-coupon` 用于优惠券、免息券、折扣券、息费优惠。
- `marketing-benefit` 用于会员权益、专属优惠、活动福利。
- 营销内容模式只决定 `body` 内容，不新增弹窗类型。

## 12. 场景映射

```txt
结果告知 / 规则说明 / 额度解释:
  type: alert
  action: single-action

高风险确认 / 授权确认 / 扣费确认 / 删除确认:
  type: confirm
  action: double-action 或 stacked-action

需要用户填写信息:
  type: form
  action: single-action

额度通过 / 可借额度 / 核审通过:
  type: marketing
  pattern: marketing-amount
  action: single-action

优惠券 / 免息券 / 折扣券 / 息费优惠:
  type: marketing
  pattern: marketing-coupon
  action: single-action 或 stacked-action

会员权益 / 专属优惠 / 活动福利:
  type: marketing
  pattern: marketing-benefit
  action: single-action 或 stacked-action

选择列表 / 协议说明 / 更多操作:
  type: bottom-sheet
  action: optional

超长规则说明:
  type: alert / bottom-sheet
  body: scrollable
```

## 13. AI 生成流程

```txt
1. 判断是否需要打断当前流程。
   - 不需要打断：不要使用 Modal / Popup。
   - 需要打断：继续判断类型。

2. 判断弹窗类型。
   - 告知说明：alert
   - 明确决策：confirm
   - 表单填写：form
   - 营销权益：marketing
   - 底部选择或更多操作：bottom-sheet

3. 如果是 marketing，判断内容模式。
   - 额度通过 / 可借额度 / 核审通过：marketing-amount
   - 优惠券 / 免息券 / 折扣券 / 息费优惠：marketing-coupon
   - 会员权益 / 专属优惠 / 活动福利：marketing-benefit

4. 判断内容长度。
   - 短内容：height hug-content
   - 长内容：body scrollable，container max-height 540px

5. 判断按钮组合。
   - 单一确认：single-action
   - 二选一决策：double-action
   - 主次差异强：stacked-action

6. 判断 close 是否出现。
   - single-action 且主按钮文案为「我知道了」或「好的」：hide close。
   - single-action 且主按钮为业务行动，如「立即使用优惠」「立即开通会员」「去认证」：show close。
   - double-action / stacked-action：按场景是否允许关闭、跳过或稍后处理判断。

7. 应用 Token 与布局规则。
```

## 14. 文案规则

- 标题必须明确表达弹窗目的，不写泛化标题。
- 标题建议不超过 11 个中文字符。
- 正文只说明原因、影响和下一步，不堆叠多个无关信息。
- 风险、金额、期限、权益可使用 `color-text-highlight` 强调。
- 按钮文案必须是动作，例如“确认”“继续”“去认证”“返回首页”。
- 不使用“好的呢”“温馨提示一下”等口语化文案。

## 15. 禁止项

- 不要用普通 Card 模拟弹窗。
- 不要临时创建弹窗背景、遮罩、圆角、阴影或按钮样式。
- 不要使用旧项目 token 或旧文本样式名。
- 不要将关闭按钮放进正文流式布局。
- 不要让超长正文撑出视口。
- 不要在弹窗内放多个无关主题。
- 不要在未明确需要决策时默认使用双按钮。
