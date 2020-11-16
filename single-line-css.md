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
Now, as you increase or decrease the screen size, these flex items both shrink and grow.

### Sidebar Says: grid-template-columns: minmax(<min>, <max>) …)
This demo takes advantage of the minmax function for grid layouts. What we're doing here is setting the minimum sidebar size to be 150px, but on larger screens, letting that stretch out to 25%. The sidebar will always take up 25% of its parent's horizontal space until that 25% becomes smaller than 150px. Add this as a value of grid-template-columns with the following value: minmax(150px, 25%) 1fr. The item in the first column (the sidebar in this case) gets a minmax of 150px at 25%, and the second item (the main section here) takes up the rest of the space as a single 1fr track.
```
.parent {
  display: grid;
  grid-template-columns: minmax(150px, 25%) 1fr;
}
```

### Pancake Stack: grid-template-rows: auto 1fr auto
Unlike the Deconstructed Pancake, this example does not wrap its children when the screen size changes. Commonly referred to as a sticky footer, this layout is often used for both websites and apps, across mobile applications (the footer is commonly a toolbar), and websites (single page applications often use this global layout). Adding display: grid to the component will give you a single column grid, however the main area will only be as tall as the content with the footer below it. To make the footer stick to the bottom, add:
```
.parent {
  display: grid;
  grid-template-rows: auto 1fr auto;
}
```
This sets the header and footer content to automatically take the size of its children, and applies the remaining space (1fr) to the main area, while the auto sized row will take the size of the minimum content of its children, so as that content increases in size, the row itself will grow to adjust.

### Classic Holy Grail Layout: grid-template: auto 1fr auto / auto 1fr auto 
For this classic holy grail layout, there is a header, footer, left sidebar, right sidebar, and main content. It's similar to the previous layout, but now with sidebars! To write this entire grid using a single line of code, use the grid-template property. This enables you to set both the rows and columns at the same time. The property and value pair is: grid-template: auto 1fr auto / auto 1fr auto. The slash in between the first and second space-separated lists is the break between rows and columns.
```
.parent {
  display: grid;
  grid-template: auto 1fr auto / auto 1fr auto;
}
```
As in the last example, where the header and footer had auto-sized content, here the left and right sidebar are automatically sized based on their children's intrinsic size. However, this time it is horizontal size (width) instead of vertical (height).

### 12-Span Grid: grid-template-columns: repeat(12, 1fr)
Next we have another classic: the 12-span grid. You can quickly write grids in CSS with the repeat() function. Using: repeat(12, 1fr); for the grid template columns gives you 12 columns each of 1fr.
```
.parent {
  display: grid;
  grid-template-columns: repeat(12, 1fr);
}

.child-span-12 {
  grid-column: 1 / 13;
}
```
Now you have a 12 column track grid, we can place our children on the grid. One way to do this would be to place them using grid lines. For example, grid-column: 1 / 13 would span all the way from the first line to the last (13th) and span 12 columns. grid-column: 1 / 5; would span the first four.

Another way to write this is by using the span keyword. With span, you set the starting line and then how many columns to span into from that starting point. In this case, grid-column: 1 / span 12 would be equivalent to grid-column: 1 / 13, and grid-column: 2 / span 6 would be equivalent to grid-column: 2 / 8.

```
.child-span-12 {
  grid-column: 1 / span 12;
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


