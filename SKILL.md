---
name: toc-design-system
description: 金融信贷产品 Mobile / H5 UI 设计规范库。Use when generating, reviewing, or implementing financial lending H5 pages, mobile UI screens, Figma page layouts, design tokens, component rules, and AI-generated UI pages.
---

# TOC Design System

Use this skill for financial lending product UI work, especially Mobile / H5 page generation, Figma screen generation, design review, and frontend implementation guidance.

## Core Rule

All generated UI must follow the design system documents in this repository. Do not invent temporary colors, font sizes, spacing, radii, shadows, icons, components, or page patterns when an existing rule applies.

## Reading Order

When generating or reviewing a page, read the documents in this order:

1. `skills/ui-page-generation/DESIGN_TOKENS.md`
2. `skills/ui-page-generation/theme-presets.md`
3. `skills/ui-page-generation/theme-scope.md`
4. `skills/ui-page-generation/PAGE_RULES.md`
5. `skills/ui-page-generation/COMPONENT_RULES.md`
6. Only the relevant component docs in `skills/ui-page-generation/docs/components/`

Do not read unrelated component docs unless the current page uses that component.

## Page Generation Rules

- Use `PAGE_RULES.md` as the only page-level entry point.
- Use `DESIGN_TOKENS.md` as the source of all color, typography, spacing, radius, shadow, z-index, motion, and numeric text decisions.
- Use `theme-presets.md` and `theme-scope.md` for brand theme selection, scene theme scope, theme fallback, and theme switching boundaries.
- Use `COMPONENT_RULES.md` for global component constraints, component selection, background layers, foreground contrast, numeric font rules, and component gap handling.
- Use component docs to decide component internal layout, states, variants, icon usage, and token mapping.

## Must Follow

- Prefer semantic tokens over primitive values.
- Do not hardcode a value if an existing token can express it.
- Do not create new tokens automatically.
- Do not create new component variants automatically.
- Do not create new `theme-brand-*` or `theme-scene-*` names automatically.
- Do not enable scene themes from words like member, VIP, activity, or benefit unless the module explicitly declares a scene theme.
- Do not use `div` or arbitrary shapes to simulate existing components.
- Use `AmountText` rules for standalone financial amounts, credit limits, rates, and key numeric values.
- Use `font-family-number` for numeric characters according to the rules.
- Use `assets/icons/` and `Icon.md` for icons. Do not draw ad hoc icons.
- Keep page layout responsive to the parent container. Do not rely on fixed x/y coordinates for variable content.

## Figma Page Requirements

For complete Figma Mobile / H5 page generation:

- Use the `375px * 812px` baseline frame.
- Include `status-bar`, `page-header`, `content-layer`, and `home-indicator` unless the user explicitly asks for business content only.
- Include `bottom-tab-bar` for home pages.
- Use `action-footer` only for page types that require it.
- Ensure content avoids fixed bottom elements.
- Apply background layer fade rules when using gradients, background images, or decorative background shapes.

## Gap Handling

If a required token or component does not exist, report the gap instead of inventing a new rule.

Use the missing token format from `DESIGN_TOKENS.md` and the component gap format from `COMPONENT_RULES.md`.
