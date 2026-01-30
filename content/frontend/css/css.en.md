---
topic: css
language: en
version: 1.0
---

# CSS Interview Questions

## Available Categories

- Fundamentals
- Layout
- Selectors & Specificity
- Responsive Design
- Performance
- Architecture

## Difficulty Levels

- Easy
- Medium
- Hard

## 🧠 Question 1

**ID**: css-001  
**Title**: What is the CSS box model and what are its components?  
**Difficulty**: Easy  
**Category**: Fundamentals

### Answer 📄

The CSS box model describes how elements are structured and spaced in the layout.

Each element is represented as a rectangular box consisting of:

1. **Content** – The actual text or media
2. **Padding** – Space between content and border
3. **Border** – Surrounds padding and content
4. **Margin** – Space outside the border

By default, `width` and `height` apply only to the content box.

Using:

```css
box-sizing: border-box;
```

Changes the calculation so padding and border are included in the declared width and height.

Understanding the box model is essential for layout control.

## 🧠 Question 2

**ID**: css-002  
**Title**: What is the difference between `block`, `inline`, and `inline-block` display values?  
**Difficulty**: Easy  
**Category**: Layout

### Answer 📄

### `block`

- Takes full width available
- Starts on a new line
- Can set width and height

Examples: `div`, `p`, `section`

### `inline`

- Takes only as much width as content
- Does not start on a new line
- Cannot set width and height

Examples: `span`, `a`, `strong`

### `inline-block`

- Does not start on a new line
- Can set width and height
- Respects padding and margin

Used when elements need inline positioning but block behavior.

## 🧠 Question 3

**ID**: css-003  
**Title**: What is specificity in CSS and how is it calculated?  
**Difficulty**: Medium  
**Category**: Fundamentals

### Answer 📄

Specificity determines which CSS rule is applied when multiple rules target the same element.

Specificity hierarchy:

1.  Inline styles
2.  IDs
3.  Classes, attributes, pseudo-classes
4.  Elements and pseudo-elements

Example:

```css
#main {
  color: red;
}
.container p {
  color: blue;
}
```

The ID selector wins because it has higher specificity.
Specificity is calculated as a four-part value:
Inline → IDs → Classes → Elements
Higher value wins. If equal, the later rule in the stylesheet applies.

## 🧠 Question 4

**ID**: css-004  
**Title**: What is the difference between `position: relative`, `absolute`, `fixed`, and `sticky`?  
**Difficulty**: Medium  
**Category**: Layout

### Answer 📄

### `relative`

- Positioned relative to its normal position
- Remains in document flow

### `absolute`

- Removed from document flow
- Positioned relative to the nearest positioned ancestor

### `fixed`

- Positioned relative to the viewport
- Does not move during scrolling

### `sticky`

- Behaves like `relative` until a threshold
- Then behaves like `fixed` within its container

Positioning controls element layering and layout behavior.

## 🧠 Question 5

**ID**: css-005  
**Title**: What is the difference between Flexbox and Grid?  
**Difficulty**: Medium  
**Category**: Layout

### Answer 📄

Flexbox and Grid are layout systems but solve different problems.

### Flexbox

- One-dimensional layout
- Controls layout in a row OR column
- Best for alignment and distribution of items

Used for:

- Navigation bars
- Centering content
- Small component layouts

### Grid

- Two-dimensional layout
- Controls rows AND columns simultaneously
- Designed for full page layouts

Used for:

- Complex page structures
- Responsive grids
- Layout systems

**Flexbox is content-first.**  
**Grid is layout-first.**

## 🧠 Question 6

**ID**: css-006  
**Title**: What is the CSS cascade and how does the browser decide which rule to apply?  
**Difficulty**: Medium  
**Category**: Fundamentals

### Answer 📄

The CSS cascade is the algorithm used to determine which style rule applies when multiple rules target the same element.

The browser resolves conflicts in this order:

1. **Origin** (user agent, user styles, author styles)
2. **Importance** (`!important`)
3. **Specificity**
4. **Source order** (last declared wins)

Understanding the cascade is essential for debugging unexpected styling behavior.

## 🧠 Question 7

**ID**: css-007  
**Title**: What is a stacking context and how is it created?  
**Difficulty**: Hard  
**Category**: Layout

### Answer 📄

A stacking context controls how elements are layered along the z-axis.

A new stacking context is created when:

- An element has `position` other than static AND `z-index` is set
- `opacity` is less than 1
- `transform` is applied
- `filter`, `perspective`, `will-change`, etc. are used

Elements inside a stacking context are layered independently of elements outside it.

Understanding stacking context is crucial for solving z-index issues.

## 🧠 Question 8

**ID**: css-008  
**Title**: What is the difference between `overflow: hidden`, `auto`, and `scroll`?  
**Difficulty**: Medium  
**Category**: Layout

### Answer 📄

The `overflow` property controls what happens when content exceeds its container.

- `hidden` → Content is clipped, no scrollbars
- `auto` → Scrollbars appear only if needed
- `scroll` → Scrollbars always visible

Overflow can also create a new block formatting context (BFC), affecting layout behavior.

## 🧠 Question 9

**ID**: css-009  
**Title**: What is a Block Formatting Context (BFC) and why is it useful?  
**Difficulty**: Hard  
**Category**: Layout

### Answer 📄

A Block Formatting Context (BFC) is a layout mechanism that controls how block elements interact.

A BFC is created when:

- `overflow` is not visible
- `display: flow-root`
- `float` is used
- `position: absolute` or `fixed`

Benefits:

- Prevents margin collapsing
- Contains floating elements
- Creates isolated layout environments

BFC is often used to fix layout bugs involving floats or collapsing margins.

## 🧠 Question 10

**ID**: css-010  
**Title**: What is margin collapsing and when does it occur?  
**Difficulty**: Medium  
**Category**: Layout

### Answer 📄

Margin collapsing occurs when vertical margins of adjacent block elements combine into a single margin.

It happens when:

- Two sibling block elements have vertical margins
- A parent and its first/last child both have vertical margins

The resulting margin equals the larger of the two, not their sum.

Margin collapsing does NOT occur in flex or grid containers.

## 🧠 Question 11

**ID**: css-011  
**Title**: What is the difference between `em`, `rem`, `%`, `vh`, and `vw` units?  
**Difficulty**: Medium  
**Category**: Fundamentals

### Answer 📄

CSS provides multiple relative units.

- `em` → Relative to the font-size of the parent
- `rem` → Relative to the root (`html`) font-size
- `%` → Relative to the parent element
- `vh` → 1% of viewport height
- `vw` → 1% of viewport width

Use `rem` for consistent scaling across components.  
Use viewport units for responsive layouts.

---

## 🧠 Question 12

**ID**: css-012  
**Title**: What is the difference between `min-width`, `max-width`, and `width`?  
**Difficulty**: Medium  
**Category**: Layout

### Answer 📄

- `width` sets the base width of an element
- `min-width` defines the minimum allowed width
- `max-width` defines the maximum allowed width

If constraints conflict:

- `min-width` overrides `max-width`
- `min-width` can override `width`

These properties are essential for responsive design.

---

## 🧠 Question 13

**ID**: css-013  
**Title**: What is the difference between `reflow` (layout) and `repaint` in CSS rendering?  
**Difficulty**: Hard  
**Category**: Performance

### Answer 📄

When styles change, the browser may trigger:

### Reflow (Layout)

- Recalculates element positions and dimensions
- More expensive
- Triggered by changes to layout-affecting properties (width, height, position)

---

### Repaint

- Updates visual appearance without changing layout
- Less expensive
- Triggered by changes like color or background

Frequent reflows can significantly hurt performance.

Optimizing CSS includes minimizing layout-triggering changes.

## 🧠 Question 14

**ID**: css-014  
**Title**: What are CSS Custom Properties (CSS Variables) and what are their advantages?  
**Difficulty**: Medium  
**Category**: Fundamentals

### Answer 📄

CSS Custom Properties allow you to store and reuse values throughout your stylesheet.

Syntax:

```css
:root {
  --primary-color: #3498db;
  --spacing: 16px;
}

.button {
  background: var(--primary-color);
  padding: var(--spacing);
}
```

Advantages:

- Can be changed dynamically with JavaScript
- Inherit through the cascade
- Scoped to elements (unlike preprocessor variables)
- Enable theming and dynamic styling

Unlike Sass/Less variables, CSS variables are evaluated at runtime.

## 🧠 Question 15

**ID**: css-015  
**Title**: What are CSS logical properties and why are they important?  
**Difficulty**: Medium  
**Category**: Responsive Design

### Answer 📄

Logical properties allow layout control based on writing direction rather than physical direction.

Instead of:

```css
margin-left
padding-right
```

Use:

```css
margin-inline-start
padding-inline-end
```

Benefits:

- Better internationalization (RTL/LTR support)
- More adaptable layouts
- Cleaner responsive design

Logical properties make layouts direction-aware.
