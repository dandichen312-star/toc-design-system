# Input 输入框

## 1. 用途与边界

Input 用于用户输入或展示单个字段内容，例如姓名、手机号、验证码、身份证号、银行卡号、金额、密码、备注等。

Input 只定义单个字段的容器形态、输入类型、状态、后缀能力和格式化规则。字段分组、字段间距、校验触发、错误文案位置和提交按钮由 `Form.md` 定义。

规则：

- Input 是字段控件，不承载表单分组。
- 多个 Input 的排列、分割线和卡片分组由 Form 负责。
- 选择类字段可先使用 `suffix: arrow` 表达，后续需要复杂选择时独立为 Picker / Select。

## 2. 容器形态

```txt
field-row:
  用途：表单行输入，左 label + 右 control。
  场景：联系人、银行卡、认证资料。

field-box:
  用途：独立输入框，整块白底圆角容器。
  场景：登录、单字段填写、弹窗表单。

textarea:
  用途：多行文本输入。
  场景：备注、地址、原因说明、补充资料。
```

规则：

- `field-row` 用于 FormCard 内的行式字段，字段之间的分割线由 Form / Card 规则决定。
- `field-box` 用于独立输入控件，不承担多个字段分组。
- `textarea` 高度由内容或 Form 规则决定，不使用单行 Input 高度。

## 3. 输入类型

```txt
text：普通文本，例如姓名、公司名。
tel：手机号、联系电话。
captcha：短信验证码、图形验证码。
id-card：身份证号。
bank-card：银行卡号。
amount：金额输入。
number：普通数字，不包含金额语义。
password：登录密码、交易密码、支付密码。
textarea：多行文本。
```

规则：

- 手机号使用 `tel`。
- 验证码使用 `captcha`。
- 身份证号使用 `id-card`。
- 银行卡号使用 `bank-card`。
- 金额输入使用 `amount`，金额展示使用 `AmountText`。
- 地址、备注、原因说明使用 `textarea`。
- 不允许用 `text` 代替有明确业务类型的输入。

## 4. 结构

```txt
InputField
├── label 可选
├── control
│   ├── prefix 可选
│   ├── value / placeholder
│   └── suffix 可选
└── message 可选
```

元素：

```txt
label:
  用途：字段名称，例如姓名、手机号、验证码。
  样式：text-input / color-text-primary。

prefix:
  用途：区号、金额符号。
  宽度：hug-content。

value:
  用途：输入值。
  样式：text-input-value / color-text-primary。
  宽度：fill。

placeholder:
  用途：空值提示。
  样式：text-input / color-text-tertiary。
  宽度：fill。

suffix:
  用途：清除、箭头、编辑、拍卡、说明、验证码按钮、倒计时、单位、密码显隐。
  宽度：hug-content。

message:
  用途：辅助说明或错误文案。
  样式：helper 使用 text-body-sm / color-text-tertiary；error 使用 text-body-sm / color-text-danger。

field-row-group:
  用途：承载同一组 field-row。
  label-column-width: auto by longest label in group。
  content-column: fill。
  suffix-column: hug-content / fixed。
```

规则：

- `value / placeholder` 是输入主体，宽度使用 `fill`。
- `prefix / suffix` 使用 `hug-content`，不挤压输入主体。
- `message` 靠近对应字段展示；在完整表单中由 FormItem 承载。
- 同一个 `field-row-group` 内，所有 `field-row` 必须共享同一个 `label-column-width`。
- `label-column-width` 由该组内最长 label 的实际宽度决定。
- label 文案左对齐，`value / placeholder` 永远从同一个 x 起点开始并左对齐。
- 不允许因为 label 长短不同导致输入内容起点不一致。

## 5. 状态

```txt
default
focused
filled
error-empty
error-invalid
disabled
readonly
loading
countdown
```

规则：

- `default`：未输入，显示 placeholder。
- `focused`：正在输入，可显示 clear。
- `filled`：已有输入值。
- `error-empty`：未输入必填项报错。
- `error-invalid`：已输入但校验失败。
- `field-row` / FormItem 中的字段级错误可在字段下方展示 `message`。
- `field-box` 独立输入框的输入结果校验失败使用 `Toast.md` 的 `message` 提示，不在输入框下方展示 inline error。
- `disabled`：不可点击、不可输入。
- `readonly`：可展示值，不可编辑。
- `loading`：校验中、验证码发送中。
- `countdown`：验证码倒计时中。

## 6. 尺寸与布局

```txt
single-line:
  height: 60px
  width: fill
  radius: radius-input
  padding-x: spacing-16

special-line:
  height: 72px
  width: fill
  radius: radius-input
  padding-x: spacing-16

textarea:
  min-height: 96px
  width: fill
  padding: spacing-16
  divider: follow Card divider rules
```

规则：

- 默认单行 Input 高度为 `60px`。
- 特殊 Input 可放宽到 `72px`，例如验证码、银行卡、带复杂 suffix 的输入。
- Input 宽度由父容器决定，使用 `fill / 100%`。
- 单行 Input 圆角使用 `radius-input`。
- Input 容器内左右 padding 使用 `spacing-16`。
- `field-row` 横向布局遵守 `COMPONENT_RULES.md`：label-column 固定，content-column 使用 `fill`，suffix-column 使用 `hug-content / fixed`。
- 多行 Input 不临时创造分割线样式，分割线遵守 `Card.md` 的分割线规范。

## 7. Token 使用

```txt
字段标签：color-text-primary / text-input
输入文字：color-text-primary / text-input-value
占位文字：color-text-tertiary / text-input
禁用文字：color-text-disabled / text-input
输入框背景：color-bg-card
输入框边框：color-border-default
聚焦边框：color-border-brand
错误边框：color-border-danger
输入框圆角：radius-input
内部 padding：spacing-16
辅助说明：color-text-tertiary / text-body-sm
错误说明：color-text-danger / text-body-sm
```

文字规则：

- Input 内 label、placeholder、prefix、suffix 文本使用 `text-input`，字号为 `15px`。
- 输入完成后的结果文本使用 `text-input-value`，字号为 `15px`，字重为 Medium。
- 验证码操作文案属于 suffix 文本，使用 `text-input-value / color-text-brand`。

数字规则：

- 输入内容中的数字字符使用 `font-family-number`。
- 中文、英文、符号和单位仍使用组件原本字体。
- 金额输入使用 `Input amount`，不使用 `AmountText` 的大字号样式。
- 金额输入中金额符号 `¥ / ￥` 与单位 `元` 互斥，不允许同时出现。

## 8. Suffix 能力

```txt
clear:
  用途：清空当前输入。
  出现：focused / filled。
  图标：assets/icons/icon-clear.svg。

arrow:
  用途：进入选择器或下一层。
  场景：关系、开户银行、城市、职业。
  图标：assets/icons/icon-arrow-right.svg。

edit:
  用途：编辑只读信息。
  场景：预留手机号、资料修改。
  图标：assets/icons/icon-edit.svg。

camera:
  用途：拍卡、扫描银行卡。
  场景：银行卡号识别。
  图标：assets/icons/icon-camera.svg。

info:
  用途：字段说明。
  场景：规则提示、帮助说明。
  图标：assets/icons/icon-info.svg。

captcha-action:
  用途：获取验证码。
  状态：default / loading / countdown / resend。
  宽度：hug-content。
  折行：false。

countdown:
  用途：验证码倒计时。
  示例：59s。
  宽度：hug-content。
  折行：false。

unit:
  用途：单位，例如 元、期、%。

password-toggle:
  用途：密码显隐切换。
  图标：assets/icons/icon-eye.svg / assets/icons/icon-eye-off.svg。
```

规则：

- suffix 不参与输入内容。
- suffix 与输入主体横向排列，suffix 使用 `hug-content`。
- 验证码按钮文案和倒计时属于 `captcha-action`，不新增按钮样式。
- 验证码文案和倒计时不允许折行；空间不足时压缩输入主体区域，不压缩 suffix。
- suffix 图标必须引用 `Icon.md` 和 `assets/icons/` 中的资源，不允许临时绘制。
- Input 内所有 suffix 图标默认使用 `icon-md / 16px`。
- Input 内 suffix 图标点击区域使用 `24px`，图标在点击区域内居中。
- 不允许同一个 Input 组件内混用 `16px`、`18px`、`20px` 图标尺寸。

## 9. 格式化规则

```txt
tel:
  keyboard: tel
  format: 3-4-4

captcha:
  keyboard: number
  length: 按业务定义
  suffix: captcha-action

id-card:
  keyboard: text
  length: 18
  allow: number + X
  X: uppercase

bank-card:
  keyboard: number
  format: 4 位分组
  suffix: camera 可选

amount:
  keyboard: decimal
  format: 千分位
  decimal: 按业务定义

number:
  keyboard: number

password:
  suffix: password-toggle

```

规则：

- 格式化不改变原始提交值。
- `amount` 是输入态，不等同于金额展示态。
- `id-card` 的 `X` 必须大写展示。

## 10. 场景映射

```txt
姓名 / 公司名 / 联系人姓名:
  type: text

手机号 / 联系电话 / 预留手机号:
  type: tel

短信验证码:
  type: captcha
  suffix: captcha-action / countdown

身份证号:
  type: id-card

银行卡号:
  type: bank-card
  suffix: camera 可选

借款金额 / 还款金额 / 提前还款金额:
  type: amount

登录密码 / 交易密码 / 支付密码:
  type: password

关系 / 开户银行 / 城市 / 职业:
  type: text
  suffix: arrow
  note: 复杂选择后续使用 Picker / Select

备注 / 地址 / 原因说明:
  type: textarea
```

## 11. AI 生成流程

```txt
1. 判断字段是输入还是选择。
   - 可直接键盘输入：使用 Input。
   - 需要列表选择：Input + suffix arrow，或记录 Picker / Select 缺口。

2. 判断容器形态。
   - 表单卡片内行式字段：field-row。
   - 独立输入框：field-box。
   - 多行内容：textarea。

3. 判断输入类型。
   - 手机号：tel。
   - 验证码：captcha。
   - 身份证：id-card。
   - 银行卡：bank-card。
   - 金额：amount。

4. 判断 suffix 能力。
   - 可清除：clear。
   - 选择：arrow。
   - 验证码：captcha-action / countdown。
   - 银行卡扫描：camera。

5. 判断状态和错误反馈位置。
   - 空值：default。
   - 输入中：focused。
   - 已输入：filled。
   - FormItem 字段级校验失败：error-empty / error-invalid + inline message。
   - field-box 独立输入结果校验失败：error-invalid + Toast message。
   - 不可编辑：disabled / readonly。

6. 应用 Token 与布局规则。
```

## 12. 禁止项

- 不允许直接使用原生 input 样式替代项目输入框。
- 不允许临时创造输入框边框色、背景色、圆角、高度或字号。
- 不允许用 `text` 代替明确的 `tel`、`captcha`、`id-card`、`bank-card`、`amount` 类型。
- 不允许把 Form 分组、提交按钮、整组校验流程写进 Input。
- 不允许把金额输入画成 `AmountText` 展示样式。
