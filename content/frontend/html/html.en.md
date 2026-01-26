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

## 🧠 Question 1

**ID**: html-001  
**Title**: What is the difference between `<div>` and `<span>`?  
**Difficulty**: Easy  
**Category**: Fundamentals

### Answer 📄

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

## 🧠 Question 2

**ID**: html-002  
**Title**: What is the purpose of the `doctype` declaration?  
**Difficulty**: Easy  
**Category**: Fundamentals

### Answer 📄

The `<!DOCTYPE>` declaration tells the browser which version of HTML the document is written in.

Its main purposes are:

- Enables standards mode in modern browsers
- Prevents browsers from rendering the page in quirks mode
- Ensures consistent layout and CSS behavior

## 🧠 Question 3

**ID**: html-003  
**Title**: What is the difference between block and inline elements?  
**Difficulty**: Easy  
**Category**: Fundamentals

### Answer 📄

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

## 🧠 Question 4

**ID**: html-004  
**Title**: What are semantic HTML elements?  
**Difficulty**: Easy  
**Category**: Fundamentals

### Answer 📄

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

## 🧠 Question 5

**ID**: html-005  
**Title**: What is the difference between `id` and `class`?  
**Difficulty**: Easy  
**Category**: Fundamentals

### Answer 📄

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

## 🧠 Question 6

**ID**: html-006  
**Title**: What is the purpose of the `alt` attribute in `<img>` tags?  
**Difficulty**: Easy  
**Category**: Semantic & Accessibility

### Answer 📄

The `alt` attribute provides alternative text for an image when it cannot be displayed or when assistive technologies are used.

Key purposes:

- **Accessibility**: Screen readers read the alt text for visually impaired users
- **SEO**: Search engines use alt text to understand image content
- **Fallback**: Displays text if the image fails to load

Best practice:

- Be descriptive but concise
- Use `alt=""` for decorative images

Example:

```html
<img src="profile.jpg" alt="Portrait of Jane Doe smiling" />
```

## 🧠 Question 7

**ID**: html-007  
**Title**: Explain semantic HTML elements like `<article>`, `<section>`, `<aside>`, and when to use them instead of `<div>`.  
**Difficulty**: Medium  
**Category**: Semantic & Accessibility

### Answer 📄

Semantic elements describe their meaning clearly to browsers, developers, and assistive technologies.

- `<article>`: Self-contained content that can stand alone (e.g., blog post, news story)
- `<section>`: Thematic grouping of content (e.g., chapter, introduction)
- `<aside>`: Content indirectly related to main content (e.g., sidebar, related links, ads)

Benefits over `<div>`:

- Better accessibility (screen readers announce roles)
- Improved SEO (search engines understand structure)
- More maintainable code

## 🧠 Question 8

**ID**: html-008  
**Title**: What are the differences between `<input type="number">` and `<input type="tel">`?  
**Difficulty**: Medium  
**Category**: Forms

### Answer 📄

Both input types are used for numeric-like input, but they behave differently.

**`type="number"`**

- Accepts only numeric values
- Provides built-in validation
- Shows increment/decrement arrows in some browsers
- May reject characters like "+" or "-" depending on configuration

**`type="tel"`**

- Intended for telephone numbers
- Does not enforce numeric validation
- Triggers numeric keypad on mobile devices
- Allows flexible formatting (e.g., +1-800-123-4567)

Use `type="tel"` for phone numbers and `type="number"` for actual numeric data.

## 🧠 Question 9

**ID**: html-009  
**Title**: How can you improve page performance using HTML attributes or techniques?  
**Difficulty**: Medium  
**Category**: Performance

### Answer 📄

Several HTML features help optimize loading and rendering:

- Use `loading="lazy"` on `<img>` and `<iframe>` for deferred loading
- Add `async` or `defer` to `<script>` tags to avoid blocking render
- Use `<link rel="preload">`, `preconnect`, or `dns-prefetch` for critical resources
- Specify `width` and `height` on images to prevent layout shifts (CLS)
- Use responsive images with `srcset` and `<picture>`

These techniques improve load time, reduce blocking, and enhance user experience.

Example:

```html
<img src="large.jpg" loading="lazy" width="800" height="600" alt="..." />
<script src="app.js" defer></script>
```

## 🧠 Question 10

**ID**: html-010  
**Title**: What is the `<meta name="viewport">` tag and why is it important for responsive design?  
**Difficulty**: Easy  
**Category**: Browser Behavior

### Answer 📄

The viewport meta tag controls how a webpage is displayed on mobile devices.  
Without it, mobile browsers often render pages at a desktop width and scale them down.

Standard usage:

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
```

- `width=device-width`: Matches the device's screen width
- `initial-scale=1.0`: Sets initial zoom level

It is essential for responsive web design.
