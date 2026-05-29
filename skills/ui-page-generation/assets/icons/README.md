# Icon Assets

SVG icons for `ui-page-generation`. All icons follow `docs/components/Icon.md`.

## Style

- Base icons: `viewBox="0 0 24 24"` (toast: `0 0 32 32`)
- Outline, `stroke-width="1.5"`, round caps/joins
- `stroke="currentColor"` / `fill="currentColor"` where needed
- Empty-state / brand logo may use custom viewBox and fill
- No text labels in SVG; `aria-hidden="true"` on root `<svg>`

## Base icons (`Icon.md` §5)

| File | Semantic |
|------|----------|
| `icon-info.svg` | Info |
| `icon-arrow-right.svg` | Enter / next |
| `icon-back.svg` | Back |
| `icon-clear.svg` | Clear input |
| `icon-edit.svg` | Edit |
| `icon-camera.svg` | Camera |
| `icon-search.svg` | Search |
| `icon-eye.svg` | Show password |
| `icon-eye-off.svg` | Hide password |
| `icon-close.svg` | Close |
| `icon-check.svg` | Check / selected mark |
| `icon-message.svg` | Message |

## Page & component icons (`Icon.md` §5.1)

| File | Semantic |
|------|----------|
| `icon-tab-home.svg` | Tab home (default) |
| `icon-tab-home-active.svg` | Tab home (active) |
| `icon-tab-account.svg` | Tab account (default) |
| `icon-tab-account-active.svg` | Tab account (active) |
| `icon-status-waiting.svg` | Result waiting |
| `icon-status-success.svg` | Result success |
| `icon-status-fail.svg` | Result fail |
| `icon-checkbox-default.svg` | Checkbox empty (circle) |
| `icon-checkbox-selected.svg` | Checkbox checked (circle + check) |
| `icon-task-auth.svg` | Task card / auth |
| `icon-task-profile.svg` | Task card / profile |
| `card-task-default.svg` | Task card fallback |
| `icon-benefit-limit.svg` | Benefit / limit |
| `icon-benefit-coupon.svg` | Benefit / coupon |
| `icon-product-default.svg` | Product placeholder |

## Brand & business icons (`Icon.md` §5.2)

| File | Semantic |
|------|----------|
| `home-brand-logo.svg` | Home header / hero brand logo |
| `icon-address.svg` | Address / location |
| `icon-customer-servic.svg` | Customer service (legacy filename) |
| `icon-notice-bar-default.svg` | Global notice bar icon |
| `icon-notice-bar-default-1.svg` | Notice bar icon variant |

## Empty state icons (`Icon.md` §5.3)

| File | Semantic |
|------|----------|
| `icon-empty-network.svg` | No network |
| `icon-empty-notice.svg` | No messages |
| `icon-empty-bankcard.svg` | No bank card |
| `icon-empty-coupon.svg` | No coupon |
| `icon-empty-cardpackage.svg` | No card package |
| `icon-empty-loan-record.svg` | No loan record |

## Toast icons (`Toast.md`)

| File | Semantic |
|------|----------|
| `toast-info.svg` | Toast info |
| `toast-warning.svg` | Toast warning |
| `toast-loading.svg` | Toast loading (spin in CSS) |

## Usage

Reference from HTML previews or implementation:

```html
<img src="./.cursor/skills/ui-page-generation/assets/icons/icon-close.svg" alt="" />
```

Color is controlled by CSS `color` on the parent or `filter` — SVG uses `currentColor` where applicable.
