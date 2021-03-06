# CSS
Contains snippet for both CSS and SCSS
## Button states
```scss
// order is important: hover, focus, active
.active {
    background: none;       // original state

    &:hover {
      background: blue;     // hover
    }

    &:focus {
      background: green;    // right after clicked / left
    }

    &:active {
      background: red;      // currently being clicked
    }
}
```
## SCSS Maps
```scss
$array: (
  a: 20px,
  b: 40px,
  c: 60px
);

.test {
  height: map-get($array, a);
}
```
## Favourite order
```json
{
  "order/order": [
      "at-rules",
      "custom-properties",
      "dollar-variables",
      "declarations",
      "rules"
  ],
  "order/properties-order": [

      "display",
      "position",
      "top",
      "right",
      "bottom",
      "left",
      "float",
      "visibility",
      "opacity",
      "z-index",
      "clear",
      "overflow",

      "flex",
      "flex-direction",
      "align-self",
      "align-items",
      "justify-content",

      "width",
      "min-width",
      "max-width",
      "height",
      "min-height",
      "max-height",
      "margin",
      "margin-top",
      "margin-right",
      "margin-bottom",
      "margin-left",
      "padding",
      "padding-top",
      "padding-right",
      "padding-bottom",
      "padding-left",

      "border",
      "border-radius",
      "border-top",
      "border-right",
      "border-bottom",
      "border-left",
      "border-width",
      "border-top-width",
      "border-right-width",
      "border-bottom-width",
      "border-left-width",
      "border-style",
      "border-top-style",
      "border-right-style",
      "border-bottom-style",
      "border-left-style",
      "border-color",
      "border-top-color",
      "border-right-color",
      "border-bottom-color",
      "border-left-color",

      "background",
      "background-color",
      "background-image",
      "background-repeat",
      "background-position",

      "list-style",
      "caption-side",

      "table-layout",
      "border-collapse",
      "border-spacing",
      "empty-cells",
      "vertical-align",

      "font",
      "font-family",
      "font-size",
      "font-weight",
      "text-align",
      "text-indent",
      "text-transform",
      "text-decoration",
      "line-height",
      "word-spacing",
      "letter-spacing",
      "white-space",
      "color",

      "content",
      "quotes"
  ]
}
```
