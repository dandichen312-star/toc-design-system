# FormItem 表单行

## 1. 用途与边界

FormItem 用于承载表单或列表中的一行字段，适用于资料填写、认证信息、银行卡信息、联系人信息、基础资料选择等高频场景。

FormItem 负责一行字段的标题、内容、说明、右侧操作和状态展示。多个 FormItem 的分组、提交按钮和整体校验流程由 `Form.md` 定义。

规则：

- FormItem 是“一行字段”，不是完整表单。
- 可键盘输入的内容引用 `Input.md`。
- 独立金额展示引用 `AmountText.md`。
- 按钮引用 `Button.md`，图标引用 `Icon.md`。
- 不单独拆 `ListItem`、`Picker`、`Checkbox` 文档，当前阶段统一由 FormItem 承载高频行式场景。

## 2. 类型

```txt
text-row:
  用途：标题 + 文本值。
  场景：姓名、银行卡信息、认证资料展示。

input-row:
  用途：标题 + 可输入控件。
  场景：手机号、验证码、身份证号、金额输入。

picker-row:
  用途：标题 + 占位 / 已选值 + arrow。
  场景：婚姻、学历、职业、月收入、开户地址。
  点击后：打开 PickerSheet.md。

action-row:
  用途：标题 / 说明 + 操作按钮。
  场景：去认证、去还款、获取验证码、重新提交。

check-row:
  用途：标题 / 说明 + checkbox / radio。
  场景：勾选协议、单选项、列表选择。

icon-row:
  用途：图标 + 标题 + 描述 + 操作。
  场景：银行卡、车辆、资料项、权益项。

collapse-row:
  用途：分组标题 + 展开 / 收起。
  场景：基础信息、补充信息、更多资料。
```

## 3. 结构

```txt
FormItem
├── leading 可选：icon / checkbox / radio
├── left-area：label / title / description
├── right-area：value / placeholder / Input / picker / status / button / icon / checkbox / radio
├── suffix 可选：arrow
└── message 可选：helper / error
```

元素：

```txt
leading:
  宽度：fixed / hug-content。
  图标：引用 Icon.md。

left-area:
  样式：text-input / color-text-primary。
  宽度：hug-content / fill。
  对齐：left。

right-area:
  样式：text-input / text-input-value。
  宽度：hug-content / fill。
  对齐：right。

suffix:
  宽度：fixed。
  对齐：right。

message:
  样式：helper 使用 text-body-sm / color-text-tertiary；error 使用 text-body-sm / color-text-danger。
```

规则：

- 表单场景中，`left-area` 承载标题和说明，始终居左、左对齐。
- 表单场景中，`right-area` 承载所有可操作内容，始终居右、右对齐。
- 可输入控件、选择值、展开收起、勾选、按钮、图标、状态都归入 `right-area`。
- `suffix: arrow` 固定在最右侧，不能挤压 `left-area`。
- 协议类整行勾选可以把 checkbox 放在 `leading`；表单项的勾选 / 单选状态放在 `right-area`。
- `message` 只用于字段级辅助说明或错误，不承载业务主内容。

## 4. 尺寸与布局

```txt
single-line:
  height: 60px
  width: fill

double-line:
  height: 72px
  width: fill

special-line:
  height: 80px
  width: fill

divider:
  follow Card divider rules
```

规则：

- 默认单行 FormItem 高度为 `60px`。
- 双行标题 / 描述使用 `72px`。
- 特殊场景可放宽到 `80px`，例如状态说明、还款期数、右侧双行内容。
- `double-line` 不是把单行内容垂直居中后拉高，而是 `title + description` 的上下结构。
- 当右侧也出现 `title + description`、`status + action-button` 等双层内容时，使用 `special-line: 80px`。
- 双行左侧内容默认左对齐；右侧双层内容默认右对齐，并整体贴近 `suffix`。
- 右侧 `suffix: arrow` 放在最右侧，不能插入到右侧双层文案中间。
- 右侧状态 + 按钮组合中，状态文案在上，按钮在下，二者整体右对齐。
- 同一个 FormCard / FormSection 内，左侧标题从同一个 x 起点开始。
- 右侧可操作内容从右侧对齐，不能因为左侧标题长度不同而错位。
- FormItem 宽度自适应父容器，使用 `fill / 100%`。

## 5. 状态

```txt
default
selected
disabled
readonly
error
expanded
collapsed
```

规则：

- `selected` 用于选中项、单选项、勾选项。
- `disabled` 不可点击。
- `readonly` 可展示值，不可编辑。
- `error` 必须展示靠近字段的错误文案，或由 Form 触发 Toast。
- `expanded / collapsed` 只用于 `collapse-row`。

## 6. Token 使用

```txt
标题：text-input / color-text-primary
已选值 / 输入值：text-input-value / color-text-primary
占位文字：text-input / color-text-tertiary
说明文字：text-body-sm / color-text-tertiary
错误文案：text-body-sm / color-text-danger
背景：color-bg-card
分割线：遵守 Card.md 分割线规则
图标：遵守 Icon.md
按钮：遵守 Button.md
```

数字规则：

- 行内数字字符使用 `font-family-number`。
- 独立金额、额度、利率主数字使用 `AmountText`。
- 倒计时、日期、期限等行内数字遵守 `COMPONENT_RULES.md` 的行内数字高亮规则。

## 7. 场景映射

```txt
姓名 / 手机号 / 身份证号:
  type: input-row 或 text-row

验证码:
  type: input-row
  control: Input captcha

婚姻 / 学历 / 职业 / 月收入 / 开户银行:
  type: picker-row
  suffix: arrow
  interaction: open PickerSheet

银行卡号:
  type: input-row 或 text-row
  suffix: camera 可选

预留手机号:
  type: text-row
  suffix: edit 可选

协议 / 单选项 / 多选项:
  type: check-row

列表选择:
  type: check-row 或 picker-row

资料分组标题:
  type: collapse-row

带图标信息项:
  type: icon-row
```

## 8. AI 生成流程

```txt
1. 判断这一行是输入、选择、展示、操作、勾选还是折叠。
2. 如果需要键盘输入，使用 input-row + Input。
3. 如果需要点击选择，使用 picker-row + arrow。
4. 如果只是展示信息，使用 text-row。
5. 如果需要右侧按钮，使用 action-row + Button。
6. 如果需要勾选或单选，使用 check-row。
7. 如果是分组展开收起，使用 collapse-row。
8. 应用 left-area 左对齐、right-area 右对齐、suffix fixed。
```

## 9. 禁止项

- 不要为每个业务场景新增一个 FormItem 类型。
- 不要在 FormItem 中临时绘制图标、按钮或输入框。
- 不要把完整表单提交逻辑写进 FormItem。
- 不要让同组字段的输入内容起点不一致。
- 不要用 Input 表达必须点击选择的字段，选择字段使用 `picker-row`。
