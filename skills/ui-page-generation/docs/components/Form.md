# Form 表单

## 1. 用途

Form 用于信息填写、资料认证、登录注册、绑卡、申请流程、还款确认等需要用户输入、选择并提交的场景。

Form 负责组织 `FormItem`、校验信息、辅助说明和提交操作。

## 2. 常见结构

```txt
Form
├── FormSection
│   └── FormItem
│       ├── Label
│       ├── Control
│       ├── HelperText
│       └── ErrorMessage
└── FormAction
```

## 3. 状态

```txt
default
editing
submitting
disabled
error
success
```

本项目不使用绿色成功色。成功或普通反馈优先使用信息提示语义。

## 4. Token 使用

```txt
表单标签：color-text-primary / text-body-md
辅助说明：color-text-tertiary / text-body-sm
错误文案：color-text-danger / text-body-sm
表单项间距：spacing-form-gap
字段内部间距：spacing-list-gap
分组卡片背景：color-bg-card
分组卡片圆角：radius-card
提交按钮：Button primary
次要按钮：Button secondary 或 text
```

## 5. 布局规则

- 表单字段应按业务含义分组。
- 重要字段优先展示在前。
- 长表单应拆分为多个 section。
- 提交按钮应位于表单末尾或页面底部固定操作区。
- 错误信息必须靠近对应字段。
- 同一个 FormCard / FormSection 内的行式字段必须共享同一个 label-column-width。
- label-column-width 由该组内最长 label 的实际宽度决定。
- 所有字段的输入内容必须从同一个 x 起点开始并左对齐。
- suffix 操作区固定在右侧，不挤压 label-column。

## 6. AI 使用规则

- 表单字段必须由 `FormItem.md` 承载，并有清晰 label 或 placeholder。
- 必填项必须有明确提示。
- 错误状态必须展示错误文案。
- 金额字段使用 Input `amount`，金额展示使用 AmountText。
- 提交操作使用 Button `primary`。
- 不同业务分组应使用卡片或分组标题。
- 不允许混用多套表单样式。
- 不允许用临时布局拼接表单项。
