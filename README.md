# CSS Grid playground

Based on the [Pluralsight course](https://app.pluralsight.com/library/courses/css-grid-creating-layouts/) "Creating Layouts with CSS Grid" by Matt Henry.

*Coding web layouts has never been easy until now. This course will teach you CSS Grid, a technology to define rational layouts for your websites that is finally ready to go mainstream.*

- [04-grid](./src/04-grid/12-column.html): Apply grid basic concepts. The folder [concept](./src/04-grid/concept/) contains just the concept behind the website.

- [05-grid](./src/05-grid/12-column.html): Improve the grid, removing micro managed definitions.

- [06-grid-responsive](./src/06-grid-responsive/12-column.html): Make the grid *responsive* using *grid areas* and *media queries*.

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
  - `fractional unit` (`fr`) stay at `min-content` until all other tracks reach their growth limit. For ex. if `column-1` is defined as `minmax(100px, 200px)`, `fr` will stay `min-content` until column-1 reaches `200px`, then the extra-space available is splitted between all columns.
  - `auto` is the default value, is basically defined as `minmax(min-content, max-content)`.
  This means that the extra space will not be distribuited to `auto` columns.
  *Auto grows past its growth limit only if there are no fractional unit (fr) tracks competing with it.*

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

### Grid track positioning

- absolute

```css
[grid container] {
 grid-column-start: 1;

 /* or -1 for a 12-cols grid */
 grid-column-end: 13; 
```

- relative with `span`: instructs a grid to span a certain number of tracks

```css
[grid container] {
 grid-column-start: span 2;
 or
 grid-column-end: span 2;
}
```

*NB. It's not a suggested practice, but in this way you can also make items overlap each other. Then use `z-index` to adjust the visibility: with a value > 0 the item will go above, with < 0, below.*

### Grid-column, grid-row, grid-area shorthands

- grid-column:

```css
[grid container] {
 /* starts at 1, ends at 3 */
 grid-column: 1 / 3; 
 or
 /* starts when it needs, span for 2 columns */
 grid-column: span 2;
}
```

- same for grid-row:

```css
[grid container] {
 /* starts at 1, ends at 3 */
 grid-row: 1 / 3; 
}
```

- both together with grid-area:

```css
[grid container] {
 grid-area: <start row> / <start col> / <end row> / <end col>;

 /* starts at row 1 / col 2, ends at row 3 / col 6 */
 grid-area: 1 / 2 / 3 / 6;

 /* same as */
 grid-row: 1 / 3; 
 grid-column: 2 / 6;
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

## Item alignment

You can only align an item when it's inside a container that has extra space.

### Align all elements of a grid (center, space-around, space-between, start, flex-start, end, flex-end, ...)

- `justify` means horizontal, left-right direction, main-axis
- `align` means vertical, top-bottom direction, cross-axis

So:

- `justify-content` (default: start >> top-left)
- `align-content` (default: start >> top-left)
- (more info on CSS Box alignment)

```css
[grid container] {
 /* horizontal, left-right direction, main-axis */
 justify-content: space-around;
 /* vertical, top-bottom direction, cross-axis */
 align-content: center;
}
```

- `dense`: If a grid has an empty space (for example, because of some span properties) you can fill that gap using `grid-auto-flow: dense`. The source order will be then un-ordered.

```css
[grid container] {
 display: grid:
 grid: auto-flow 5em / repeat(4, 1fr);
 grid-auto-flow: dense;
}

#item8  {
 grid-column: span 3;
}
```

- `order`: Each item has a default order of 0. Item5 will be positioned after all the items with default order, and item11 before them instead.

```css
#item5  {
 order: 1;
}

#item11  {
 order: -1;
}
```

*NB. `dense` and `order` are not a suggested option because of accessibility (ex. tab order).*

### Align content in a cell (stretch, start, center, end)

- `justify-items` (default: stretch)
- `align-items` (default: stretch)

```css
[grid container] {
 /* horizontal, left-right direction */
 justify-items: center;
 /* vertical, top-bottom direction */
 align-items: center;
}
```

### Align content of individual elements in a cell

- `justify-self`
- `align-self`

```css
[#special-item] {
 justify-self: end;
 align-self: end;
}
```

### Naming grid lines

You can name grid lines using `[a-name]`. You can assign multiple names - separated by a space - to a line too.

```css
[grid container] {
 /* 4 columns, but remember there are 5 vertical lines! */
 grid-template-columns: [left-edge] 1fr 1fr [midpoint] 1fr 1fr [right-edge];
 /* 4 rows, but remember there are 5 horizontal lines! */
 grid-template-rows: [header-start] 2em 5em [header-end body-start] 10em 10em [body-end];
}

... and then refer to them...

header {
 grid-column: left-edge / right-edge
}
```

Can also be used inside a `repeat`, then you will have multiple grid lines with the same name. You can refere to the the N instance of the grid name

```css
[grid container] {
    grid-template-columns: [left-edge] repeat(auto-fill, [block-start] 10em 3em [block-end]) [right-edge];
}

#article1 {
 /* this refers to the 2nd instance of block-start, and the 3rd instance of block-end */
 grid-column: block-start 2 / block-end 3;
}

#article2 {
 /* this refers to the 2nd instance of block-start, and span until the 2nd instance of block-end it come across */
 grid-column: block-start 2 / span 2 block-end;
}
```

*NB. Be carefull using grid names with `auto-fill`, as some blocks cannot exist anymore because of resizing (then the page will crash).*

### Naming grid areas

```css
[grid container] {
 grid-template-areas: "header header header"
                         "nav main aside"
                         "footer footer footer";
 grid-template-rows: min-content auto min-content;
 grid-template-columns: 15em 1fr 1fr;
}

header {
 grid-area: header;
}
```

- implicitly creates `[header-start]` and `[header-end]`, etc named grid lines (and viceversa: grid lines following the naming convention ...-start, ...-end creates implicitly grid areas)
- use ellipsis `...` to specify an empty area
- each row must have the same number of cells. This definition will not work:

```css
[grid container] {
    grid-template-areas: "header"                   <- 1
                         "nav main"                 <- 2
                         "sidebar sidebar sidebar"; <- 3
}
```

This will work instead:

```css
[grid container] {
    grid-template-areas: "header ... ..."           <- 3
                         "nav main ..."             <- 3
                         "sidebar sidebar sidebar"; <- 3
}
```

- supports only rectangular/squared areas, no "L" shaped. This `sidebar` definition will not work:

```css
[grid container] {
    grid-template-areas: "header header header"
                         "sidebar main aside"
                         "sidebar sidebar sidebar";
}
```

### Grid named areas using grid shorthand

but not the easiest to understand...

```css
[grid container] {
 grid: "header header header" min-content 
       "nav main aside" auto 
       "footer footer footer" min-content / 
       15em 1fr 1fr;
}
```

However a better way is to split the area names and grid size definition. 
Be carefully that `grid` will override `grid-template-areas` with the default values (empty name), so `grid-template-areas` must be placed after `grid`:

```css
[grid container] {
 grid: min-content auto min-content / 15em 1fr 1fr; <- grid size
 grid-template-areas: "header header header"        <- and then the area names
                      "sidebar main aside"
                      "sidebar sidebar sidebar";
}
```
