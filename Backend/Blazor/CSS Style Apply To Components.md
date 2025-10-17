# CSS Style Apply to components

Wrap components with a `<div>` and using the `::deep` pseudo-class in a CSS selector

For example:

html:

```html
<div>
  <MudText>test</MudText>
</div>
```

css:

```css
div ::deep .mud-text {
  // some style
}
```
