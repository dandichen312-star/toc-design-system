# Tabs 标签页

## 1. 用途

Tabs 用于同级内容切换，例如产品类型、记录类型、账单状态、权益分类等。

Tabs 不用于流程步骤，不用于层级导航。

## 2. 类型

```txt
line
pill
segment
```

## 3. 状态

```txt
active
inactive
disabled
```

## 4. Token 使用

```txt
选中文字：color-text-brand
未选中文字：color-text-secondary
禁用文字：color-text-disabled
指示器颜色：color-brand-500
标签文字：text-body-md
弱背景：color-bg-disabled
圆角：radius-full 或 radius-card
```

## 5. 类型使用规则

```txt
line：
  常规顶部切换，适合内容区分类。

pill：
  强调选中项，适合卡片内或运营模块。

segment：
  二到三个选项的紧凑切换。
```

## 6. AI 使用规则

- Tabs 只用于同级内容切换。
- 不用于流程步骤。
- 当前选中态必须清晰。
- 选项数量过多时需要考虑横向滚动或其他筛选方式。
- 不允许临时创建选中态颜色、指示器颜色或字号。
