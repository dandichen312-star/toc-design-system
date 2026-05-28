# PickerSheet 底部选择弹层

## 1. 用途与边界

PickerSheet 用于表单流程中点击选择字段后的底部选择弹层，适用于婚姻、学历、职业、月收入、开户地址、开户银行等高频单选场景。

规则：

- `FormItem.md` 的 `picker-row` 只负责表单入口和已选值展示。
- PickerSheet 负责点击后的选择容器、选项列表、选中态和关闭 / 确认行为。
- 基础版只定义普通列表单选，不包含搜索、多选和完整级联选择。
- `cascade` 作为后续扩展能力预留，不在基础版中绘制或详细定义。

## 2. 类型

```txt
instant-single:
  用途：即时单选。
  行为：点击选项后立即回填 FormItem 并关闭弹层。
  场景：婚姻、学历、简单职业分类。

confirm-single:
  用途：确认单选。
  行为：点击选项后进入 selected 状态，点击确定后回填并关闭。
  场景：月收入、开户地址、开户银行等需要用户二次确认的选择。
```

## 3. 结构

```txt
PickerSheet
├── overlay 必填
├── sheet 必填
│   ├── header 必填
│   │   ├── cancel 可选
│   │   ├── title 必填
│   │   ├── confirm 可选
│   │   └── close 可选
│   ├── option-list 必填
│   │   └── option-item
│   └── safe-area-bottom 必填
```

顶部规则：

```txt
instant-single:
  header: title + close
  title-align: left 或 center
  close: Icon.md / close

confirm-single:
  header: cancel + centered title + confirm
  cancel: text-body-md / color-text-secondary
  confirm: text-body-md / color-text-brand
```

## 4. 选项结构

```txt
option-item
├── main-text 必填
├── description 可选
└── selected-icon 可选
```

规则：

- 单行选项只展示 `main-text`。
- 多行选项展示 `main-text + description`。
- `selected-icon` 使用 `Icon.md` 的 `check` 图标。
- 选项右侧不放 arrow；PickerSheet 内部是结果选择，不是下一层跳转。

## 5. 尺寸与布局

```txt
sheet:
  width: fill / 100%
  max-height: viewport-height * 70%
  radius: radius-sheet top-left / top-right
  background: color-bg-card

header:
  height: 56px
  padding-x: spacing-16

option-item:
  single-line-height: 60px
  double-line-height: 72px
  padding-x: spacing-16

option-list:
  item-count <= 5: hug-content
  item-count > 5: scroll

bottom:
  padding-bottom: safe-area-bottom
```

规则：

- 小于等于 5 个选项时，弹层高度由内容自适应。
- 超过 5 个选项时，`option-list` 内部滚动。
- 弹层最大高度为屏幕高度的 `70%`。
- 底部必须包含 `safe-area-bottom`，不额外叠加 `spacing-24`。
- `header` 固定在顶部；列表滚动时 header 不随列表滚动。

## 6. 状态

```txt
default
selected
disabled
loading
```

规则：

- `selected` 表示当前已选项。
- `disabled` 表示选项不可点击，常用于不满足条件的选项。
- `loading` 只用于选项数据加载中，不用于提交表单。
- `instant-single` 点击可用选项后立即关闭，不需要确定按钮。
- `confirm-single` 点击选项后只更新选中态，必须点击确定后关闭。

## 7. Token 使用

```txt
弹层背景：color-bg-card
遮罩：遵守 ModalPopup.md overlay 规则
标题：text-title-sm / color-text-primary
取消：text-body-md / color-text-secondary
确定：text-body-md / color-text-brand
选项默认文字：text-input / color-text-primary
选项选中文字：text-input-value / color-text-brand
选项说明文字：text-body-sm / color-text-tertiary
选项禁用文字：text-input / color-text-disabled
分割线：遵守 Card.md 分割线规则
关闭图标：Icon.md / close
选中图标：Icon.md / check / color-text-brand
```

数字规则：

- 选项中的数字字符使用 `font-family-number`。
- 月收入、期限、开户地址编号等行内数字遵守 `COMPONENT_RULES.md` 的全局数字规则。
- PickerSheet 中的普通选项数字不使用 `AmountText.md`。

## 8. 场景映射

```txt
婚姻 / 学历:
  type: instant-single
  header: title + close
  option: single-line

职业 / 月收入:
  type: confirm-single
  header: cancel + title + confirm
  option: single-line 或 double-line

开户地址 / 开户银行:
  type: confirm-single
  header: cancel + title + confirm
  option-list: 超过 5 项时滚动

省市区 / 多级地址:
  type: cascade
  status: reserved
```

## 9. AI 生成流程

```txt
1. 判断 FormItem picker-row 点击后是否需要选择弹层。
2. 简单轻选择使用 instant-single。
3. 金额区间、地址、银行等需要确认的选择使用 confirm-single。
4. 根据选项内容判断单行 60px 或多行 72px。
5. 选中项使用 color-text-brand + check icon。
6. 选项数 <= 5 时弹层自适应高度。
7. 选项数 > 5 时 option-list 滚动，sheet 最大高度 70%。
8. 底部只保留 safe-area-bottom。
```

## 10. 禁止项

- 不要用 Modal 普通弹窗表达表单选择列表。
- 不要把 `FormItem picker-row` 画成可展开的内联列表。
- 不要在基础版中加入搜索框。
- 不要在基础版中加入多选逻辑。
- 不要临时绘制 check、close 等图标，必须引用 `Icon.md`。
- 不要让选项列表超过最大高度后撑高整个页面。
