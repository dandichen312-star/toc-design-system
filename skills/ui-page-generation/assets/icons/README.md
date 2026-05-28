# Icon Assets

Place fixed component icons in this directory.

## Base Icons

Common component icons must follow `docs/components/Icon.md`.

Required base files:

```txt
icon-info.svg
icon-arrow-right.svg
icon-clear.svg
icon-edit.svg
icon-camera.svg
icon-search.svg
icon-eye.svg
icon-eye-off.svg
icon-close.svg
```

Requirements:

- SVG format
- 24px viewBox
- Outline style unless component rules explicitly say otherwise
- `stroke="currentColor"` or `fill="currentColor"`
- No background
- Do not include text labels

## Toast Icons

Required files:

```txt
toast-info.svg
toast-warning.svg
toast-loading.svg
```

Requirements:

- SVG format
- 32px viewport recommended
- No background
- Prefer `currentColor` for stroke or fill
- Do not include text labels
- `toast-loading.svg` should be suitable for spin motion
