# Tag 标签

## 1. 用途

Tag 用于状态、权益、活动、风险、分类、说明等短文本标识。

Tag 只表达辅助信息，不替代正文说明。

## 2. 类型

```txt
default
brand
highlight
warning
danger
```

## 3. 状态

```txt
default
disabled
```

## 4. Token 使用

```txt
默认标签文字：color-text-secondary
品牌标签文字：color-text-brand
高亮标签文字：color-text-highlight
警告标签文字：color-warning-500
危险标签文字：color-danger-500
标签圆角：radius-tag
标签文字：text-caption
```

## 5. 内容规则

- 标签文案必须短，通常不超过 6 个中文字符。
- 标签应放在被标识内容附近。
- 同一区域标签数量不宜过多。
- 标签不应承载完整说明文案。

## 6. AI 使用规则

- 普通分类、状态可使用 `default`。
- 品牌相关、选中强调可使用 `brand`。
- 金融权益、优惠、减免可使用 `highlight`。
- 风险提示、注意事项可使用 `warning`。
- 失败、异常、严重风险可使用 `danger`。
- 不允许临时创造标签颜色、圆角或字号。
