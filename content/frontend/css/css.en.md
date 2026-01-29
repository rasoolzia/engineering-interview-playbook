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
