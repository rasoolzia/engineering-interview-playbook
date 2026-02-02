---
topic: html
language: en
version: 1.1
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
**Title**: What is the difference between `async` and `defer` attributes on `<script>` tags? Explain their impact on the Critical Rendering Path.  
**Difficulty**: Hard  
**Category**: Performance

### Answer 📄

Both `async` and `defer` allow non-blocking script loading, but they differ in execution timing:

- **async**:
  - Downloads in parallel
  - Executes as soon as download finishes (may interrupt HTML parsing)
  - No guarantee of order between multiple async scripts
  - Good for independent scripts (analytics, ads)

- **defer**:
  - Downloads in parallel
  - Executes only after HTML parsing is complete (just before DOMContentLoaded)
  - Preserves script order
  - Ideal for scripts that depend on DOM (most app scripts)

**Impact on Critical Rendering Path (CRP)**:

- Without attributes → render-blocking (parsing pauses)
- async → may still block render if executes early
- defer → truly non-blocking for rendering

Best practice: Use `defer` for most cases unless you need immediate execution.

Example:

```html
<script src="analytics.js" async></script>
<script src="app.js" defer></script>
```

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
**Title**: What are some common ARIA mistakes developers make, and how should you prioritize native HTML over ARIA?  
**Difficulty**: Hard  
**Category**: Semantic & Accessibility

### Answer 📄

Common mistakes:

1.  Using ARIA when native HTML exists (e.g., `role="button"` on `<div>` instead of `<button>`)
2.  Adding redundant ARIA (e.g., `aria-label` on image with good `alt`)
3.  Forgetting `aria-hidden` on decorative content
4.  Incorrect live regions (`aria-live="polite"` vs `assertive`)
5.  Missing keyboard focus management for custom components

**Golden rule (ARIA Authoring Practices)**:  
**"No ARIA is better than bad ARIA"**  
**"If you can use a native semantic element, do it"**

Priority order:

1.  Native HTML (button, input, nav, etc.)
2.  ARIA roles/states only when needed
3.  JavaScript for dynamic behavior

Example bad → good:

```html
<!-- Bad -->
<div role="button" onclick="...">Click</div>

<!-- Good -->
<button onclick="...">Click</button>
```

Use tools like Lighthouse / axe to catch mistakes.

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
**Title**: How do HTML templates (`<template>`) and Shadow DOM work together in Web Components, and what problems do they solve?  
**Difficulty**: Hard  
**Category**: Browser Behavior & Modern HTML

### Answer 📄

`<template>` + Shadow DOM are core to Web Components:

- `<template>`: Parsed but inert HTML fragment (not rendered, no side effects until cloned)
- Shadow DOM: Encapsulated subtree attached to a custom element (styles/DOM isolated)

Together they solve:

- Style leakage (component CSS doesn't affect page)
- DOM encapsulation (no accidental querySelector conflicts)
- Reusability without framework (no React/Vue needed)

Basic example:

```html
<template id="my-card">
  <style>
    .card {
      border: 1px solid;
      padding: 1em;
    }
  </style>
  <div class="card"><slot name="title"></slot></div>
</template>

<script>
  class MyCard extends HTMLElement {
    constructor() {
      super();
      const shadow = this.attachShadow({ mode: 'open' });
      const template = document
        .getElementById('my-card')
        .content.cloneNode(true);
      shadow.appendChild(template);
    }
  }
  customElements.define('my-card', MyCard);
</script>

<my-card><span slot="title">Hello</span></my-card>
```

Benefits: Framework-agnostic, performant, future-proof components.

## 🧠 Question 18

**ID**: html-018  
**Title**: How does the sandbox attribute work on `<iframe>` and why is it important for security?  
**Difficulty**: Hard  
**Category**: Browser Behavior & Security

### Answer 📄

The sandbox attribute restricts what an embedded iframe can do, adding a security layer against malicious content.

Common values (space-separated):

- (empty) → full restrictions (very safe)
- `allow-scripts` → allows JS execution
- `allow-same`-origin → treats iframe as same-origin (dangerous!)
- `allow-popups` → allows new windows
- `allow-forms` → allows form submission

Default (sandbox=""): Disables:

- Navigation
- Scripts
- Forms
- Plugins
- Same-origin policy bypass

Use case: Embedding third-party content (ads, user-generated HTML, previews).

Example (safe embed):

HTML

```html
<iframe
  src="https://example.com/widget"
  sandbox="allow-scripts allow-same-origin"
></iframe>
```

Without sandbox → potential XSS or clickjacking risk.

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

## 🧠 Question 21

**ID**: html-021  
**Title**: Explain how `<picture>` + `srcset` + `sizes` work together for responsive images, and why they are better than CSS media queries for images.  
**Difficulty**: Hard  
**Category**: Performance

### Answer 📄

This trio enables art-direction and resolution switching without JavaScript:

- `<picture>`: Container with multiple `<source>` options
- `srcset`: List of image candidates (with descriptors like 1x, 2x, or widths)
- `sizes`: Tells browser expected rendered width at different media conditions

Browser picks best source based on:

- Device pixel ratio (DPR)
- Viewport width
- Supported format (e.g., WebP)

Why better than CSS media queries?

- Browser decides before download (saves bandwidth)
- No extra HTTP requests for detection
- Supports art direction (different crops per breakpoint)

Example:

```html
<picture>
  <source media="(min-width: 800px)" srcset="large.jpg 1x, large-2x.jpg 2x" />
  <source media="(min-width: 400px)" srcset="medium.jpg" />
  <img
    src="small.jpg"
    srcset="small.jpg 400w, medium.jpg 800w"
    sizes="(max-width: 400px) 100vw, 800px"
    alt="..."
  />
</picture>
```

Saves data, improves Core Web Vitals (LCP).

## 🧠 Question 22

**ID**: html-022  
**Title**: How does HTML5 form validation work, and how can you implement custom validation using the Constraint Validation API?  
**Difficulty**: Hard  
**Category**: Forms

### Answer 📄

HTML5 provides built-in form validation via attributes like `required`, `pattern`, `min/max`, and type-specific checks (e.g., email, url).

Process:

- Browser checks on submit or focusout (with `novalidate` to disable)
- Invalid fields show browser-native error bubbles
- Custom errors via JS API

**Constraint Validation API**:

- Access via `element.validity` (object with states like `valueMissing`, `patternMismatch`)
- Set custom errors: `element.setCustomValidity('Error message')` (empty string to clear)
- Trigger: `element.reportValidity()` or `form.checkValidity()`

Why hard? Handling i18n, async validation (e.g., unique username check), and polyfills for old browsers.

Example (custom email domain check):

```html
<form>
  <input id="email" type="email" required pattern="[^@]+@example\.com" />
  <button type="submit">Submit</button>
</form>

<script>
  const email = document.getElementById('email');
  email.addEventListener('input', () => {
    if (email.value.endsWith('@gmail.com')) {
      email.setCustomValidity('Only @example.com allowed');
    } else {
      email.setCustomValidity('');
    }
  });
</script>
```

This API integrates with ARIA for accessibility (e.g., auto aria-invalid).

## 🧠 Question 23

**ID**: html-023  
**Title**: How can you implement structured data in HTML using schema.org, and what benefits does it provide for SEO?  
**Difficulty**: Hard  
**Category**: SEO & Meta

### Answer 📄

Structured data uses JSON-LD, Microdata, or RDFa to mark up content with schema.org vocabulary, helping search engines understand entities (e.g., Product, Event, Recipe).

Preferred format: JSON-LD in `<script type="application/ld+json">` (easiest, no markup pollution).

Benefits:

- Rich snippets (stars, prices in SERPs)
- Better crawlability (Google, Bing use it for features like Knowledge Graph)
- Voice search/featured snippets
- Potential ranking boost (indirect via better understanding)

Challenges: Validation with Google's Structured Data Testing Tool, avoiding spam (must match visible content).

Example (Product schema):

```html
<script type="application/ld+json">
  {
    "@context": "https://schema.org",
    "@type": "Product",
    "name": "Wireless Headphones",
    "image": "headphones.jpg",
    "description": "Noise-cancelling over-ear headphones",
    "offers": {
      "@type": "Offer",
      "price": "199.99",
      "priceCurrency": "USD"
    },
    "aggregateRating": {
      "@type": "AggregateRating",
      "ratingValue": "4.5",
      "reviewCount": "89"
    }
  }
</script>
```

Implement for key pages; test with rich results tool.

## 🧠 Question 24

**ID**: html-024  
**Title**: What is the `contenteditable` attribute, what are its common pitfalls, and how can you make it accessible?  
**Difficulty**: Hard  
**Category**: Browser Behavior

### Answer 📄

contenteditable="true" makes an element editable by users (like a rich text editor).

Behavior:

- Applies to any element
- Inherited by children unless overridden
- Browser handles basic editing (bold via Ctrl+B, but inconsistent)

Pitfalls:

- Security: Sanitize input to prevent XSS (e.g., injected `<script>`)
- Inconsistent across browsers (e.g., IE/Edge vs Chrome on paste)
- No native undo stack control
- Performance with large content
- Accessibility issues (no default ARIA roles)

To make accessible:

- Add ARIA: role="textbox" or "region", aria-label, aria-multiline="true"
- Handle keyboard: focus, arrow navigation
- Use execCommand or modern Clipboard API for features

Example (simple editor):

```html
<div
  contenteditable="true"
  role="textbox"
  aria-multiline="true"
  aria-label="Editable area"
>
  Edit me!
</div>

<script>
  const editor = document.querySelector('[contenteditable]');
  editor.addEventListener('input', (e) => {
    // Sanitize: e.target.innerHTML = sanitize(e.target.innerHTML);
  });
</script>
```

For production, use libraries like Quill/ProseMirror.

## 🧠 Question 25

**ID**: html-025  
**Title**: Explain resource hints in HTML (`preload`, `prefetch`, `preconnect`, `dns-prefetch`) and when to use each for performance optimization.  
**Difficulty**: Hard  
**Category**: Performance

### Answer 📄

Resource hints (`<link rel="...">`) tell browsers to proactively fetch/resolve resources, reducing latency.

- **preload**: Fetch critical resources early (e.g., fonts, scripts needed soon). Mandatory as="type" for priority.
- **prefetch**: Fetch resources for next navigation (e.g., next page assets) – low priority, speculative.
- **preconnect**: Establish TCP connection + TLS/SSL handshake early (for third-party domains).
- **dns-prefetch**: Resolve DNS only (cheaper than preconnect, for many domains).

Order of cost: dns-prefetch (cheapest) < preconnect < prefetch < preload (highest priority).

Benefits: Faster TTFB, better FCP/LCP in Core Web Vitals.

Pitfalls: Overuse wastes bandwidth; test with Lighthouse.

Example:

```html
<!-- Preload critical font -->
<link rel="preload" href="font.woff2" as="font" type="font/woff2" crossorigin />

<!-- Preconnect to CDN -->
<link rel="preconnect" href="https://cdn.example.com" crossorigin />

<!-- DNS prefetch for analytics -->
<link rel="dns-prefetch" href="https://analytics.com" />

<!-- Prefetch next page -->
<link rel="prefetch" href="/next-page.html" />
```

Use preload for above-the-fold; prefetch for navigation flows.
