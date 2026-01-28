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

## 🧠 Question 11

**ID**: html-011  
**Title**: What is the difference between `async` and `defer` in `<script>` tags, and how do they affect parsing and rendering?  
**Difficulty**: Hard  
**Category**: Performance

### Answer 📄

By default, when the browser encounters a `<script>` tag:

1. HTML parsing pauses
2. The script is downloaded
3. The script is executed
4. Parsing resumes

This behavior makes scripts render-blocking.

---

### `async`

```html
<script src="app.js" async></script>
```

- Script downloads in parallel with HTML parsing
- Executes immediately after download
- Does NOT guarantee execution order
- May execute before DOM is fully parsed

Best for independent scripts (e.g., analytics, ads).

### `async`

```html
<script src="app.js" defer></script>
```

- Script downloads in parallel
- Executes after HTML parsing completes
- Execution order is preserved
- Runs before DOMContentLoaded

Best for application scripts that rely on DOM structure.

## 🧠 Question 12

**ID**: html-012  
**Title**: What is the difference between `<meta>` tags and HTTP headers, and when should each be used?  
**Difficulty**: Hard  
**Category**: SEO & Meta

### Answer 📄

Both `<meta>` tags and HTTP headers provide metadata about a document, but they operate at different levels.

---

### `<meta>` Tags

- Defined inside the `<head>` section of an HTML document
- Provide metadata interpreted by browsers and search engines
- Processed after the HTML document begins loading

Common examples:

```html
<meta charset="UTF-8" />
<meta name="description" content="HTML interview questions" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
```

Use cases:

- Page description for SEO
- Character encoding
- Viewport configuration

---

### HTTP Headers

- Sent by the server before the HTML document
- Control browser behavior at the protocol level
- More authoritative than meta tags

Examples:

- `Content-Type`
- `Cache-Control`
- `Content-Security-Policy`
- `Set-Cookie`

Use cases:

- Security policies
- Caching control
- Redirection
- Content negotiation

## 🧠 Question 13

**ID**: html-013  
**Title**: What is ARIA and when should it be used?  
**Difficulty**: Hard  
**Category**: Semantic & Accessibility

### Answer 📄

ARIA stands for **Accessible Rich Internet Applications**.

It is a set of attributes that enhance accessibility in complex web applications.

Example:

```html
<div role="button" aria-pressed="true"></div>
```

However, the first rule of ARIA is:

If a native semantic HTML element can solve the problem, use it instead.

Incorrect:

```html
<div role="button"></div>
```

Correct:

```html
<button></button>
```

ARIA should be used when:

- Building custom UI components
- Native HTML semantics are insufficient
- Dynamic state changes must be announced (e.g., `aria-live`)

ARIA complements semantic HTML but does not replace it.

## 🧠 Question 14

**ID**: html-014  
**Title**: What is the Critical Rendering Path and what role does HTML play in it?  
**Difficulty**: Hard  
**Category**: Performance

### Answer 📄

The Critical Rendering Path (CRP) is the sequence of steps the browser follows to render a page.

Main stages:

1.  Parse HTML → Build DOM
2.  Parse CSS → Build CSSOM
3.  Combine into Render Tree
4.  Layout
5.  Paint

HTML directly affects:

- DOM size and depth
- Resource loading order
- Blocking scripts
- Images without defined dimensions

HTML optimization techniques:

- Use `defer` for scripts
- Minimize DOM depth
- Specify `width` and `height` for images
- Preload critical resources

Understanding CRP is essential for performance optimization.

## 🧠 Question 15

**ID**: html-015  
**Title**: What is the difference between `id` and `data-*` attributes in HTML, and when should each be used?  
**Difficulty**: Medium  
**Category**: Fundamentals

### Answer 📄

Both `id` and `data-*` attributes attach information to elements, but they serve different purposes.

---

### `id`

- Must be unique within the document
- Used for:
  - Fragment navigation (`#section`)
  - JavaScript DOM selection
  - Label associations (`for` attribute)
- Has semantic meaning in document structure

Example:

```html
<section id="pricing"></section>
```

### `data-*` attributes

- Custom attributes for storing extra data
- Do not affect semantics
- Accessible via JavaScript (`element.dataset`)

Example:

```html
<button data-user-id="42"></button>
```

Use `id` for document identity.  
Use `data-*` for storing custom metadata.

## 🧠 Question 16

**ID**: html-016  
**Title**: What is the difference between `<section>` and `<div>` from a document outline perspective?  
**Difficulty**: Medium  
**Category**: Semantic & Accessibility

### Answer 📄

`<div>` is a generic container with no semantic meaning.

`<section>` represents a thematic grouping of content and contributes to the document outline.

Key differences:

- `<section>` should typically contain a heading
- It signals structure to assistive technologies and search engines
- `<div>` is purely structural with no semantic value

Use `<section>` when the content represents a logical section of the document.  
Use `<div>` only when no semantic element is appropriate.

## 🧠 Question 17

**ID**: html-017  
**Title**: What is the purpose of the `<template>` element and how does it differ from regular HTML content?  
**Difficulty**: Hard  
**Category**: Browser Behavior

### Answer 📄

The `<template>` element holds HTML content that is not rendered immediately.

Key characteristics:

- Its content is parsed but not rendered
- Not part of the active DOM
- Can be cloned and inserted via JavaScript

Example:

```html
<template id="card-template">
  <div class="card"><h3></h3></div>
</template>
```

Use cases:

- Client-side rendering
- Reusable UI fragments
- Performance optimization

Unlike hidden elements, `<template>` content does not affect layout or accessibility until explicitly added to the DOM.

## 🧠 Question 18

**ID**: html-018  
**Title**: What is the difference between `<iframe>` and embedding content using `<object>` or `<embed>`?  
**Difficulty**: Hard  
**Category**: Browser Behavior

### Answer 📄

All three elements embed external content, but they differ in capabilities and historical usage.

---

### `<iframe>`

- Embeds another HTML document
- Creates a nested browsing context
- Commonly used for videos, maps, widgets
- Supports sandboxing for security

---

### `<object>`

- Can embed various types of resources
- Historically used for plugins (e.g., Flash)
- Supports fallback content

---

### `<embed>`

- Similar to `<object>`
- Self-closing
- Historically used for multimedia plugins

Modern best practice:

- Use `<iframe>` for embedding web pages
- Avoid plugin-based embedding
- Use sandbox and proper attributes for security

## 🧠 Question 19

**ID**: html-019  
**Title**: What is the difference between `<link>` and `<a>` in HTML?  
**Difficulty**: Medium  
**Category**: Fundamentals

### Answer 📄

Both create relationships, but they serve different purposes.

---

### `<a>` (Anchor)

- Creates hyperlinks within page content
- Visible and interactive
- Used for navigation

Example:

```html
<a href="/about">About</a>
```

### `<link>`

- Defines relationships between the document and external resources
- Placed inside `<head>`
- Not visible to users

Common uses:

- Stylesheets
- Preload / Prefetch
- Icons

Example:

```html
<link rel="stylesheet" href="styles.css" />
```

`<a>` is for user navigation.  
`<link>` is for document-level resource relationships.

## 🧠 Question 20

**ID**: html-020  
**Title**: What are Web Components in HTML and what core technologies enable them?  
**Difficulty**: Hard  
**Category**: Browser Behavior

### Answer 📄

Web Components allow creation of reusable, encapsulated custom elements.

They are built on four core technologies:

1.  **Custom Elements** – Define new HTML tags
2.  **Shadow DOM** – Encapsulated DOM subtree
3.  **HTML Templates** – Reusable markup
4.  **ES Modules** – Modular JavaScript

Example concept:

```html
<user-card></user-card>
```

Benefits:

- Encapsulation
- Reusability
- Framework-independent components

Web Components enable native component architecture without relying on external frameworks.
