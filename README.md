# CSS Grid playground

Based on the [Pluralsight course](https://app.pluralsight.com/library/courses/css-grid-creating-layouts/) "Creating Layouts with CSS Grid" by Matt Henry.

*Coding web layouts has never been easy until now. This course will teach you CSS Grid, a technology to define rational layouts for your websites that is finally ready to go mainstream.*

- [01-grid](./src/01-grid/12-column.html): Apply grid basic concepts. The folder [concept](./src/01-grid/concept/) contains just the concept behind the website.

## Css grid properties

### CSS Grids

- makes an element into a grid container

```css
[grid container] {
 display: grid;
}
```

### Grid track sizes

```css
[grid container] {
 grid-template-columns: 200px 10em 30ch;
}
```

```css
[grid container] {
 grid-template-columns: 25% 25% 50%;
}
```

```css
[grid container] {
 grid-template-columns: 15em auto 15em;
}
```

```css
[grid container] {
 grid-template-columns: 25em 1fr 1fr;
}
```

- viewport-responsive: %, fr, auto
- content-responsive:
  - `min-content`: as small as possible to fit its content,
  - `max-content`: as large as necessary to contain its content,
  - `fit-content()`: fit track size to the content, but don't go above specified value
  - `minmax(<min size>, <max size>)`: minimun and maximum values for a track

```css
[grid container] {
 grid-template-columns: 1fr min-content 1fr;
}
```

```css
[grid container] {
 grid-template-columns: 1fr max-content 1fr;
}
```

```css
[grid container] {
 grid-template-columns: 1fr minmax(max-content, 50%) 1fr;
}
```

```css
[grid container] {
 grid-template-columns: 1fr fit-content(30em) fit-content(30em) 1fr;
}
```

### Grid shorthands

- 3 columns 20em each

```css
[grid container] {
 grid-template-columns: repeat(3, 20em);
}
```

- consolidate grid-template-rows and grid-template-columns

```css
[grid container] {
 grid-template: 20em 10em / repeat(6, 1fr);
}
```

- consolidate grid-template-rows and grid-template-columns and more

```css
[grid container] {
grid: 20em 10em / repeat(6, 1fr);
}
```

### grid-auto (implicitly created)

- whether the grid fills rows or columns first while assigning grid items, default: row

```css
[grid container] {
 grid-auto-flow: column;
}
```

- size for implicit created rows

```css
[grid container] {
 grid-auto-rows: 10em;
}
```

- size for implicit created columns

```css
[grid container] {
 grid-auto-columns: 10em;
}
```

- shorthand to specify which axis new tracks are added implicitly with auto-flow (rows or columns) and their size. Example for `grid-auto-columns: 10em;`

```css
[grid container] {
 grid: 10em 10em / auto-flow 10em;
}
```

`grid: 10em 10em / auto-flow 10em;`

is a concise implicit grid rule with grid:

```css
grid-template-rows: 10em 10em;
grid-auto-flow: columns;
grid-auto-columns: 10em;
```

### grid gaps

```css
[grid container] {
 grid-column-gap: 1em;
}

```css
[grid container] {
 grid-row-gap: 1em;
}
```

- concise way to specify both:

```css
[grid container] {
 grid-gap: 1em 2em;
}
```
