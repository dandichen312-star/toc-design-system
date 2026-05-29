# Agreement 协议组件

## 1. 用途与边界

Agreement 用于承载主按钮附近的协议阅读、协议确认和协议查看入口，适用于借款申请、授权确认、绑卡、实名认证、会员开通等场景。

Agreement 负责：

- 展示协议前置说明文案。
- 展示一个或多个协议名称。
- 按规则决定是否展示勾选框。
- 点击协议名称后拉起协议弹层。
- 在未勾选场景下展示轻提醒。

Agreement 不负责：

- 不替代完整协议页。
- 不替代 `ModalPopup.md` 的通用底部弹层规则。
- 不替代 `Button.md` 的按钮规则。
- 不拆出独立 `Checkbox` 组件文档；第一版勾选能力作为 Agreement 内部能力处理。

---

## 2. 组件类型

```txt
check-agreement:
  用途：带勾选框的协议组件。
  默认前置文案：请阅读并同意
  默认行为：勾选表达“已阅读”，不作为主按钮禁用条件。

plain-agreement:
  用途：不带勾选框的协议组件。
  默认前置文案：点击提交即表示您已阅读并同意
  默认行为：只承载协议说明与协议入口。
```

规则：

- 第一版 Agreement 本体只支持 `check-agreement` 和 `plain-agreement` 两种结构。
- 协议数量属于 Agreement 内部内容差异，不额外拆“单协议组件”和“多协议组件”。
- 协议弹层内部的内容变体，不属于 Agreement 本体类型。

---

## 3. 默认位置规则

```txt
default-position:
  above-button

default-gap-to-button:
  spacing-16

width:
  fill / 跟随当前内容区宽度
```

规则：

- Agreement 默认放在主按钮上方。
- Agreement 和主按钮之间默认纵向间距使用 `spacing-16`。
- Agreement 默认占满当前内容区宽度，与按钮容器同宽。
- Agreement 默认独立成块，不与 `Notice`、风险提示、活动说明混排。
- 页面没有协议需求时，Agreement 不出现，不保留空位。
- Agreement 允许进入底部操作区，但不是默认行为。
- 当页面明确要求 Agreement 进入底部操作区时，默认顺序为：Agreement 在上，按钮在下。

---

## 4. Agreement 本体结构

### 4.1 带勾选框

```txt
Agreement
├── check-control
└── content
    ├── prefix-text
    └── agreement-text-flow
        └── agreement-name 可重复
```

### 4.2 不带勾选框

```txt
Agreement
└── content
    ├── prefix-text
    └── agreement-text-flow
        └── agreement-name 可重复
```

规则：

- Agreement 默认左对齐。
- 多行时按正文自然换行。
- 带勾选框版本中，勾选框固定在最左，右侧承载整段协议文案。
- 文案换行后仍在文案区域内，不回到勾选框下方。
- Agreement 默认包含协议前置说明文案。
- 带勾选框版本默认前置文案为 `请阅读并同意`。
- 不带勾选框版本默认前置文案为 `点击提交即表示您已阅读并同意`。
- 协议名称以外的说明文案默认是普通辅助文案，不高亮。

---

## 5. 协议名称规则

```txt
agreement-name:
  clickable: true
  highlight: fixed-deep-gray
  follow-theme: false
```

规则：

- Agreement 本体中的协议名称默认使用固定深灰文字，不跟 `brand theme` 变化，也不跟 `scene theme` 变化。
- Agreement 本体中的协议名称默认只有颜色高亮，不加下划线，不加额外装饰。
- 多个协议名称都独立高亮、独立可点击。
- 多协议场景默认在一段文案中并列展示多个协议名称。
- 多协议名称之间默认不插入额外分隔符。
- 第一版不支持额外副操作，不默认增加“查看全部协议”“风险提示”“授权说明”等额外入口。

---

## 6. 勾选框规则

```txt
check-control:
  icon: Icon.md / check
  icon-size: icon-md / 16px
  touch-area: 24px
```

规则：

- 勾选框图标大小固定为 `16px * 16px`，使用 `Icon.md` 的 `check`。
- 勾选框点击热区不小于 `24px`。
- 勾选框默认描边使用 `border-width-1 + color-border-brand`。
- 勾选框默认不填充背景。
- 勾选框选中后填充 `color-brand-500`。
- 勾选框选中后对号颜色使用 `color-text-inverse`。
- 勾选框形状为圆形。
- 勾选框与协议文案之间固定使用 `spacing-8`。
- 勾选框与协议文案第一行垂直居中对齐。
- 只有点击勾选框本身，才切换勾选状态。
- 点击协议名称，只打开协议弹层，不切换勾选状态。
- 勾选框默认只表达“我已阅读”。
- 勾选状态不作为主按钮禁用条件；未勾选时主按钮仍可点击。
- 已勾选态只显示勾选状态本身，不额外强化整行文案或协议名称。

---

## 7. 轻提醒规则

```txt
tip-bubble:
  applies-to: check-agreement
  default-text: 请勾选
  position: above-checkbox
```

规则：

- 带勾选框版本允许出现未勾选轻提醒。
- 默认轻提醒形式为勾选框上方小气泡。
- 默认文案为 `请勾选`。
- 小气泡与勾选框之间默认间距使用 `spacing-2`。
- 小气泡水平中心与勾选框水平中心对齐。
- 小气泡圆角使用 `radius-4`。
- 默认触发时机为：用户点击主按钮后，若协议未勾选，则出现轻提醒。
- 轻提醒只做提示，不影响主按钮点击。
- 轻提醒默认短暂显示后自动消失。

---

## 8. 协议弹层总则

Agreement 点击协议名称后，默认拉起 `ModalPopup.md` 的 `bottom-sheet`。

### 8.1 基础结构

```txt
AgreementSheet
├── header
│   ├── title
│   └── header-action  close | back 按条件二选一
├── body
└── footer
    └── primary-action
```

规则：

- Agreement 弹层默认使用 `ModalPopup.md` 的 `bottom-sheet`。
- Agreement 弹层只允许使用 `agreement-list`、`article-content`、`document-preview` 三种内容变体。
- AI 不允许自行新增第 4 种 Agreement 弹层变体。
- 头部右侧操作区在同一时刻只显示一种：`close` 或 `back`，不并存。
- 默认显示 `close`；仅「从 `agreement-list` 进入的单个协议浏览态」显示 `back`，此时不显示 `close`。
- 点击遮罩不关闭弹层；列表态与直接打开态通过右上 `close` 关闭；从列表进入的详情态通过右上 `back` 回到列表，或通过底部主按钮关闭整个弹层。
- 点击 `close`：只关闭弹层，不勾选，不跳转，不回写任何协议状态。
- 点击 `back`：只返回 `agreement-list` 列表态，不关闭整个弹层，不勾选，不跳转，不回写任何协议状态。
- 底部主按钮固定在弹层底部操作区，不跟随正文滚动。
- 底部主按钮文案统一规则为：默认优先业务动作文案；页面未指定时，才回退为通用文案。
- 底部主按钮规格完全复用 `Button.md`，不单独创建协议按钮样式。
- 底部操作区默认包含 `safe-area-bottom`，这是全局底部弹层规则。

### 8.2 头部通用规则

```txt
header:
  title: required
  header-action: close | back 二选一
```

规则：

- 头部固定为标题居中 + 右上操作按钮（`close` 或 `back`）。
- 头部默认不放确认按钮；头部左侧不放返回、关闭或其他操作。
- 头部总标题字号固定为 `18px`，使用 `text-title-sm`；所有 Agreement 弹层变体统一，不使用 `text-title-md`。
- `agreement-list` 说明文案字号固定为 `12px`，使用 `text-body-sm`。
- 头部标题使用总标题，不跟随当前协议名称变化；从 `agreement-list` 进入详情态时，头部总标题仍保持列表态总标题（默认 `服务协议`）。
- 总标题允许页面显式提供；未指定时，可由 AI 根据内容总结，但优先使用页面提供值。
- 标题区固定高度使用当前 Agreement 弹层设计稿基准值 `60px`。该值属于结构规则，不新增 token。
- 标题单行展示，超出截断。
- 右上操作按钮固定在标题栏区域右侧，距离顶部 `spacing-8`，距离右侧 `spacing-8`。
- `close` 图标使用 `Icon.md / close + icon-sm + color-icon-tertiary`。
- `back` 图标使用 `Icon.md / back + icon-sm + color-icon-tertiary`。
- 右上操作按钮点击热区不小于 `24px`。
- Agreement 弹层头部与正文区之间**不使用**分隔线；该规则覆盖 `ModalPopup.md` 中 bottom-sheet 头部默认分隔线。

### 8.3 右上返回规则

规则：

- `agreement-list` 列表态：右上为 `close`，不显示 `back`。
- 直接打开的 `article-content` 和直接打开的 `document-preview`：右上为 `close`，不显示 `back`。
- 只有从 `agreement-list` 进入的单个协议浏览态（`article-content` 或 `document-preview`）：右上为 `back`，不显示 `close`。
- 点击 `back` 后，返回 `agreement-list` 列表态。
- 返回后保持列表原滚动位置。
- 返回后保留刚刚查看项的主题色高亮。

### 8.4 底部主按钮规则

规则：

- 弹层底部主按钮区不单独定义固定高度。
- 底部主按钮区只遵循 `Button.md` 的按钮高度规则和弹层底部内边距规则。
- 弹层底部主按钮横向规则不单独定义，完全遵循 `Button.md` 与全局布局规则。

---

## 9. 弹层内容变体

### 9.1 变体清单

```txt
agreement-list:
  用途：多协议确认场景的列表态入口

article-content:
  用途：普通单篇协议正文阅读

document-preview:
  用途：综合融资成本明示表 / 资金成本相关合同这类预览型协议
```

### 9.2 变体选择规则

规则：

- 多协议场景下，AI 必须先按数量规则判断是否进入 `agreement-list`，不能跳过这层自行改成别的结构。
- 当协议数量 `>= 3` 时，默认先进入 `agreement-list`。
- 当协议数量 `< 3` 时，默认不进入 `agreement-list`，直接进入对应协议内容。
- 当协议数量 `< 3` 但页面明确声明需要列表态时，允许使用 `agreement-list`。
- `agreement-list` 只适用于多协议确认场景，单协议场景不使用 `agreement-list`。
- `document-preview` 只允许用于“综合融资成本明示表 / 资金成本相关合同”这类预览型协议。
- 非上述场景，默认使用 `article-content`。
- 页面未明确声明内容变体时，默认回退到 `article-content`；特殊情况由人工改。
- AI 不允许把 `document-preview` 用在非“综合融资成本明示表 / 资金成本相关合同”场景。

---

## 10. agreement-list 规则

### 10.1 用途与触发

规则：

- `agreement-list` 用于多协议确认场景的第一层列表态。
- 当协议数量 `>= 3` 时，默认先进入 `agreement-list`。
- 当协议数量 `< 3` 时，只有页面显式声明，才允许使用 `agreement-list`。
- `agreement-list` 标题固定为 `服务协议`。
- 点击列表中的单个协议名称后：
  - 若该协议属于“综合融资成本明示表 / 资金成本相关合同”这类内容，则进入 `document-preview`。
  - 其他普通协议，进入 `article-content`。

### 10.2 结构

```txt
agreement-list
├── header
│   ├── title = 服务协议
│   └── close
├── description
├── agreement-list-body
│   └── agreement-name item 可重复
└── footer
    └── primary-action
```

规则：

- 标题下方说明文案为默认结构的一部分，必须有。
- 说明文案默认表达“已阅读说明 + 同意范围提示”。
- 业务允许替换为场景化文案，但默认文案方向不变。
- 默认示例文案：`我已阅读协议内容，并同意以下借款相关协议`。
- 协议列表为单列纵向列表；**每一行仅展示一条协议**，一行对应一个协议名称。
- 禁止在同一行内并列 2 个及以上协议名称；禁止为完整展示长标题而将一条协议拆成多行占满视觉行高。
- 只有协议名称文字可点击，不是整行可点。
- 协议列表项不加右侧箭头。

### 10.3 布局与尺寸

规则：

- 列表态左右边距使用 `spacing-24`，宽度随页面内容区自适应。
- 标题与说明文案之间距离使用 `spacing-20`。
- 说明文案与协议列表之间距离使用 `spacing-4`。
- 协议列表与底部主按钮区之间距离使用 `spacing-40`。
- 协议列表区占满正文可用宽度。
- 协议列表区默认顶部开始排列。
- 协议列表项字号使用 `font-size-13`。
- 协议列表项行高使用 `line-height-40`。
- 协议名称文本左对齐。
- 协议名称超出后单行截断显示 `...`。
- 协议列表项之间不加分隔线，靠 `line-height-40` 自然分开。

### 10.4 滚动规则

规则：

- 当协议数量 `> 8` 时，协议列表区进入滚动态。
- 进入滚动态后，只有协议列表区滚动，标题、说明文案、底部按钮都固定。
- 协议列表区滚动时，右侧需要保留可见滚动条。

### 10.5 交互规则

规则：

- `agreement-list` 列表态右上为 `close`，不显示 `back`。
- 从 `agreement-list` 进入的详情态右上为 `back`，不显示 `close`。
- `agreement-list` 点击底部主按钮，表示同意列表里的全部协议。
- `agreement-list` 不要求用户逐个点开协议后才能点击底部主按钮。
- 进入单个协议浏览态后，底部主按钮文案保持与列表态一致。
- 从 `agreement-list` 进入的单个协议浏览态中，底部主按钮仍表示确认 `agreement-list` 里的全部协议。
- `agreement-list` 列表项没有“已访问过”样式。
- 用户点击某个协议名称后，当前项使用主题色高亮。
- 同一组协议名称里始终只保留 `1` 个当前高亮项，新的覆盖旧的。
- 从单个协议浏览态返回列表后，保留刚刚查看项的主题色高亮。

---

## 11. article-content 规则

### 11.1 用途

规则：

- `article-content` 用于普通单篇协议正文阅读。
- 非“综合融资成本明示表 / 资金成本相关合同”类协议，默认都使用 `article-content`。
- 当协议数量 `< 3` 且不走 `agreement-list` 时，点击哪个协议名称，就进入哪一份 `article-content`。
- 进入 `article-content` 后，不允许在弹层内再切换其他协议。

### 11.2 结构

```txt
article-content
├── header
├── body
│   └── agreement-article
└── footer
    └── primary-action
```

规则：

- 头部遵循 §8.2、§8.3：总标题 `text-title-sm`（18px）；直接打开时右上 `close`，从 `agreement-list` 进入时右上 `back` 且总标题保持列表态标题。
- 正文内部允许自行出现协议标题。
- 正文区为长文连续流阅读，不单独强调正文内标题层级。

### 11.3 布局与滚动

规则：

- 正文区左右边距沿用 `spacing-24`。
- 正文区单独滚动，底部主按钮始终固定不动。
- 正文区滚动时，右侧需要有可见滚动条。
- 不需要“已读完”之类的额外按钮状态；底部主按钮始终按正常规则展示。

---

## 12. document-preview 规则

### 12.1 用途

规则：

- `document-preview` 只用于“综合融资成本明示表 / 资金成本相关合同”这类预览型协议。
- 所有 `document-preview` 头部总标题固定为 `个人贷款综合融资成本及相关合同`，字号遵循 §8.2（`text-title-sm` / 18px）。
- 头部操作遵循 §8.3：直接打开时右上 `close`；从 `agreement-list` 进入时右上 `back`，总标题仍保持 `服务协议`。
- `document-preview` 表示确认该弹层内列出的全部信息 / 全部协议。
- `document-preview` 不要求用户逐个查看完全部协议，只要弹层出现即可点击底部主按钮。

### 12.2 结构

```txt
document-preview
├── header
│   ├── title = 个人贷款综合融资成本及相关合同
│   └── close
├── body
│   ├── description 可选
│   ├── agreement-name-list 必有（单协议时可省略）
│   └── preview-container
│       └── document-card 可选
└── footer
    └── primary-action
```

规则：

- `document-preview` 的正文结构固定顺序为：说明区 → 协议名称列表 → 文档预览容器。
- 说明区允许有，但按场景决定是否出现。
- 协议名称列表默认必须出现，并作为切换 / 查看不同协议的入口。
- 当只有 `1` 个协议名称时，允许省略协议名称列表。
- 文档预览容器是泛化的文档预览承载区，可承载图片、表格截图、PDF 页预览等。
- 内部文档卡片两种都支持，但默认有“预览容器背景区 + 内部文档卡片”两层结构。
- 内部文档卡片只作为视觉承载层，用于放文档截图 / 表格 / PDF 预览，不单独承担业务交互。

### 12.3 标题与高度基准

规则：

- `document-preview` 的整体弹层基准高度使用当前设计稿基准值 `658px`。
- `658px` 适用于 `375 x 812` 设计稿，开发按适配规则换算。
- `658px` 属于当前设计稿结构基准值，不作为新增 token。
- 弹层整体高度基准固定。
- 说明区高度按内容自适应。
- 说明区与预览区之间的纵向间距固定使用 `spacing-24`。
- 预览区占据剩余高度，并且不得低于可阅读阈值；具体阈值由页面样式稿指定。

### 12.4 名称列表规则

规则：

- 协议名称列表按正文流自然换行、左对齐。
- 协议名称之间不插入额外分隔符，名称自然连续排布。
- 默认展示第一项协议对应内容。
- 首次进入时，第一个协议名称默认高亮。
- 当前高亮项就是当前选中项。
- 点击其他协议名称后，高亮切换，预览内容同步切换。
- 同一组协议名称里始终只保留 `1` 个当前高亮项。
- 未选中项与选中项同字重，只是颜色变弱。
- 协议名称列表高亮色两种都支持，但默认跟随品牌主题色。
- 顶部标题保持总标题不变，当前协议名称只在下方内容里体现。

### 12.5 预览区规则

规则：

- 说明区和协议名称列表固定在上方。
- 只有文档预览容器滚动。
- 切换不同协议名称后，文档预览容器默认回到顶部。
- 上部固定区和下部预览区之间默认有分隔线。
- 正文区采用上下不同底色区分。
- 上部固定区更接近弹层主背景；下部预览区单独作为阅读承载底。
- 内部文档卡片默认顶部对齐放置在预览区内。
- 当内部文档卡片内容较短时，仍保持顶部对齐，不做额外居中补偿。
- 内部文档卡片默认占满预览区可用宽度，按容器内边距留白。
- 文档预览容器默认只作为预览展示区，随预览区滚动，不支持单独缩放或翻页。
- 若说明区和协议名称列表较长，仍允许继续使用 `document-preview`；上部固定区不滚动，通过换行容纳；必要时压缩下部文档预览区高度。

### 12.6 底部主按钮规则

规则：

- `document-preview` 底部主按钮默认优先使用业务动作文案。
- 也允许使用通用文案，但不是默认。
- 支持倒计时态，但默认不启用。
- 启用倒计时态时，默认优先使用“业务文案 + 倒计时”。
- 正文区与底部按钮区之间不加分隔线，靠留白区分。

---

## 13. 确认与关闭交互

规则：

- 点击 `close`：只关闭弹层，不勾选、不跳转、不回写任何状态。
- 点击 `back`：只返回 `agreement-list` 列表态，不关闭整个弹层，不勾选、不跳转、不回写任何状态。
- `check-agreement` 点击弹层底部确认按钮：关闭弹层，自动勾选 Agreement 本体中的勾选框，并按当前流程进入下一页面。
- `plain-agreement` 点击弹层底部确认按钮：关闭弹层，并按当前流程进入下一页面。
- `agreement-list` 点击弹层底部确认按钮：表示同意列表中的全部协议。
- `article-content` 若来自 `agreement-list`，底部主按钮仍表示同意该列表中的全部协议。
- `document-preview` 点击弹层底部确认按钮：表示同意该弹层内列出的全部信息 / 全部协议。

---

## 14. Token 使用

```txt
前置说明文案：
  text-body-sm
  color-text-tertiary

Agreement 本体中的协议名称：
  text-body-sm
  color-text-secondary

agreement-list 说明文案：
  text-body-sm
  color-text-tertiary

agreement-list 协议列表项：
  font-size-13
  line-height-40
  color-text-primary

当前选中协议名称：
  color-text-brand

勾选框图标：
  Icon.md / check
  size: icon-md / 16px
  default-border: color-border-brand
  checked-fill: color-brand-500
  checked-icon: color-text-inverse

组件与按钮间距：
  spacing-16

轻提醒文案：
  text-caption
  color-text-inverse

轻提醒容器：
  color-bg-toast + opacity-80
  radius-4
  shadow-sm

agreement-list:
  side-gap: spacing-24
  title-description-gap: spacing-20
  description-list-gap: spacing-4
  list-button-gap: spacing-40

article-content:
  body-side-padding: spacing-24

document-preview:
  description-preview-gap: spacing-24

协议弹层：
  ModalPopup.md / bottom-sheet

协议弹层标题：
  text-title-sm
  color-text-primary

协议弹层说明文案（agreement-list / document-preview 等）：
  text-body-sm
  color-text-tertiary

协议弹层底部按钮：
  遵守 Button.md
```

规则：

- Agreement 相关的字色、字重、字号、间距、圆角必须优先来自 `DESIGN_TOKENS.md`。
- 协议弹层头部总标题固定映射 `text-title-sm`（18px）；`agreement-list` 等说明文案固定映射 `text-body-sm`（12px）。
- 协议名称固定深灰、主题高亮、说明文案、按钮间距等规则都应优先映射现有 token。
- `60px` 标题区高度和 `658px` 弹层基准高度属于当前设计稿结构基准值，不作为新增 token。
- 除用户已明确指定的结构基准值外，不额外创造新的尺寸值。
- 勾选图标的路径粗细属于图标资产实现细节，不在当前 token 体系中单独定义。

---

## 15. AI 使用规则

- 先判断当前页面是否存在协议需求；没有则不生成 Agreement。
- 有协议需求时，先判断是否需要勾选框。
- 需要勾选框时，使用 `check-agreement`。
- 不需要勾选框时，使用 `plain-agreement`。
- 默认将 Agreement 放在主按钮上方，使用 `spacing-16` 与按钮分隔。
- 默认不把 Agreement 与 `Notice`、风险提示、活动说明混成一个说明区。
- 协议名称点击后，默认拉起 `ModalPopup.md` 的 `bottom-sheet`。
- 协议弹层头部标题固定 `text-title-sm`（18px）；`agreement-list` 说明文案固定 `text-body-sm`（12px）。
- 协议弹层头部与正文之间不加分隔线。
- 头部右上同一时刻只显示 `close` 或 `back`：仅「从 `agreement-list` 进入的详情态」使用 `back`，其余态使用 `close`。
- 协议弹层只允许使用 `agreement-list`、`article-content`、`document-preview` 三种变体。
- 多协议场景必须先按数量规则判断是否进入 `agreement-list`。
- “综合融资成本明示表 / 资金成本相关合同”类内容才允许使用 `document-preview`。
- 页面未明确声明变体时，默认回退到 `article-content`。
- 直接进入 `article-content` 后，不允许在弹层内再生成协议切换能力。

---

## 16. 禁止项

- 不要新增独立的“协议按钮组件”。
- 不要把 Agreement 本体中的协议名称做成跟主题变化的 `brand` 高亮。
- 不要给 Agreement 本体中的协议名称增加下划线或额外装饰。
- 不要让整行协议文案都承担勾选热区。
- 不要把未勾选状态升级成按钮禁用逻辑。
- 不要把协议弹层改成居中弹窗或独立协议页，除非页面明确说明。
- 不要在非“综合融资成本明示表 / 资金成本相关合同”场景使用 `document-preview`。
- 不要在单协议场景使用 `agreement-list`。
- 不要在页面未声明时，自行新增第 4 种 Agreement 弹层变体。
- 不要在 Agreement 弹层头部使用 `text-title-md`（20px）作为总标题。
- 不要在 Agreement 弹层头部与正文之间增加分隔线。
- 不要在头部左侧放置返回或关闭；不要在非「从 `agreement-list` 进入的详情态」显示 `back`。
- 不要在 `back` 与 `close` 同时出现在头部右侧。
- 不要在 `agreement-list` 同一行展示 2 条及以上协议，或将 1 条协议拆成多行占满列表行。
- 不要新增未在 `DESIGN_TOKENS.md` 中定义的新字色、字重、字号、间距或圆角。
