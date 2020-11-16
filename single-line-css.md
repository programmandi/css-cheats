# Single Line CSS Layouts (https://web.dev/one-line-layouts/)

### . Super Centered: place-items: center 
For the first 'single-line' layout, let's solve the biggest mystery in all of the CSS land: centering things. I want you to know that it's easier than you think with [`place-items: center`](https://developer.mozilla.org/en-US/docs/Web/CSS/place-items).

First specify `grid` as the `display` method, and then write `place-items: center` on the same element. `place-items` is a shorthand to set both `align-items` and `justify-items` at once. By setting it to `center`, both `align-items` and `justify-items` are set to `center`.
```
.parent {
  display: grid;
  place-items: center;
}
```
This enables the content to be perfectly centered within the parent, regardless of intrinsic size.

### The Deconstructed Pancake: flex: <grow> <shrink> <baseWidth>
Next we have the deconstructed pancake! This is a common layout for marketing sites, for example, which may have a row of 3 items, usually with an image, title, and then some text, describing some features of a product. On mobile, we'll want those to stack nicely, and expand as we increase the screen size.

By using Flexbox for this effect, you won't need media queries to adjust the placement of these elements when the screen resizes.

The [`flex`](https://developer.mozilla.org/en-US/docs/Web/CSS/flex) shorthand stands for: `flex: <flex-grow> <flex-shrink> <flex-basis>`.

Because of this, if you want your boxes to fill out to their `<flex-basis>` size, shrink on smaller sizes, but not _stretch_ to fill any additional space, write: `flex: 0 1 <flex-basis>`. In this case, your `<flex-basis>` is `150px` so it looks like:
```
.parent {
  display: flex;
}

.child {
  flex: 0 1 150px;
}
```
If you _do_ want the boxes to stretch and fill the space as they wrap to the next line, set the `<flex-grow>` to `1`, so it would look like:
```
.parent {
  display: flex;
}

.child {
  flex: 1 1 150px;
}
```

### Sidebar Says: grid-template-columns: minmax(<min>, <max>) …)
```
.parent {
  display: grid;
  grid-template-columns: minmax(150px, 25%) 1fr;
}
```

### Pancake Stack: grid-template-rows: auto 1fr auto
```
.parent {
  display: grid;
  grid-template-rows: auto 1fr auto;
}
```

### Classic Holy Grail Layout: grid-template: auto 1fr auto / auto 1fr auto 
```
.parent {
  display: grid;
  grid-template: auto 1fr auto / auto 1fr auto;
}
```

### 12-Span Grid: grid-template-columns: repeat(12, 1fr)
```
.parent {
  display: grid;
  grid-template-columns: repeat(12, 1fr);
}

.child-span-12 {
  grid-column: 1 / 13;
}
```

### RAM (Repeat, Auto, MinMax): grid-template-columns(auto-fit, minmax(<base>, 1fr))
```
.parent {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
}
```
```
.parent {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(150px, 1fr));
}
```

### Line Up: justify-content: space-between 
```
.parent {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}
```

### Clamping My Style: clamp(<min>, <actual>, <max>)
```
.parent {
  width: clamp(23ch, 50%, 46ch);
}
```

### Respect for Aspect: aspect-ratio: <width> / <height>
```
.video {
  aspect-ratio: 16 / 9;
}
```
```
.square {
  aspect-ratio: 1 / 1;
}
```


