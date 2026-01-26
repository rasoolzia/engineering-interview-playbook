---
topic: html
language: en
version: 1.0
---

# HTML Interview Questions

## Available Categories

- Fundamentals
- Semantic & Accessibility
- Forms
- SEO & Meta
- Browser Behavior
- Performance

## Difficulty Levels

- Easy
- Medium
- Hard

---

## Question 1

**ID**: html-001  
**Title**: What is the difference between `<div>` and `<span>`?  
**Difficulty**: Easy  
**Category**: Fundamentals

### Answer

`<div>` and `<span>` are generic container elements, but they differ in their display behavior and typical usage.

**`<div>`**

- Block-level element
- Takes full available width
- Starts on a new line
- Used to group larger sections of content

**`<span>`**

- Inline element
- Takes only as much width as necessary
- Does not start on a new line
- Used to group small pieces of inline content

## Question 2

**ID**: html-002  
**Title**: What is the purpose of the `doctype` declaration?  
**Difficulty**: Easy  
**Category**: Fundamentals

### Answer

The `<!DOCTYPE>` declaration tells the browser which version of HTML the document is written in.

Its main purposes are:

- Enables standards mode in modern browsers
- Prevents browsers from rendering the page in quirks mode
- Ensures consistent layout and CSS behavior

## Question 3

**ID**: html-003  
**Title**: What is the difference between block and inline elements?  
**Difficulty**: Easy  
**Category**: Fundamentals

### Answer

Block and inline elements differ in how they are displayed in the layout.

**Block-level elements**

- Start on a new line
- Take the full available width
- Can contain other block and inline elements

Examples: `<div>`, `<p>`, `<section>`

**Inline elements**

- Do not start on a new line
- Take only as much width as needed
- Typically contain text or other inline elements

Examples: `<span>`, `<a>`, `<strong>`

## Question 4

**ID**: html-004  
**Title**: What are semantic HTML elements?  
**Difficulty**: Easy  
**Category**: Fundamentals

### Answer

Semantic HTML elements clearly describe their meaning in a human- and machine-readable way.

They help:

- Improve accessibility
- Improve SEO
- Make code more maintainable

Examples of semantic elements:

- `<header>`
- `<nav>`
- `<main>`
- `<article>`
- `<section>`
- `<footer>`

Unlike `<div>`, semantic elements describe the role of the content they contain.

## Question 5

**ID**: html-005  
**Title**: What is the difference between `id` and `class`?  
**Difficulty**: Easy  
**Category**: Fundamentals

### Answer

`id` and `class` are attributes used to identify HTML elements, but they differ in scope and usage.

**`id`**

- Must be unique within a page
- Used to target a single element
- Often used for JavaScript selection or anchor links

**`class`**

- Can be reused on multiple elements
- Used to group elements with similar styling
- Commonly used in CSS

An element can have multiple classes but only one id.
