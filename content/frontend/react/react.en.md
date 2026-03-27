---
topic: react
language: en
version: 1.0
---

# React Interview Questions

## Available Categories

- React Basics
- JSX & Rendering
- Components
- Props & State
- Hooks
- Effects & Lifecycle
- Forms & Events
- Context API
- State Management
- Performance Optimization
- Rendering Behavior
- Concurrent React
- Server Components
- SSR / Hydration
- Architecture & Patterns
- React Internals
- Edge Cases & Pitfalls

## Difficulty Levels

- Easy
- Medium
- Hard

## 🧠 Question 1

**ID**: react-001
**Title**: What is React and what problem does it solve?
**Difficulty**: Easy
**Category**: React Basics

### Answer 📄

React is an open-source JavaScript library developed by Meta (Facebook) for building user interfaces, primarily single-page applications.

It addresses several core frontend challenges:

- **Keeping the UI in sync with state** — React makes the view a pure function of state. When state changes, React re-renders the relevant parts of the UI automatically.
- **Efficient DOM updates** — React uses a Virtual DOM to minimize expensive real DOM operations by computing the minimal set of changes needed.
- **Reusable UI components** — the component model lets developers compose complex UIs from small, isolated, and testable pieces.

React is intentionally focused only on the view layer. Routing, data fetching, and state management are handled by the surrounding ecosystem (React Router, TanStack Query, Zustand, Redux, etc.).

Because React is a library rather than a framework, it integrates easily into existing applications and gives teams full control over architectural decisions.

## 🧠 Question 2

**ID**: react-002
**Title**: What is the Virtual DOM and how does React use it?
**Difficulty**: Easy
**Category**: Rendering Behavior

### Answer 📄

The Virtual DOM (VDOM) is a lightweight in-memory representation of the real DOM tree. It is a plain JavaScript object tree that describes the UI structure.

When a component's state or props change, React:

1. **Renders** a new Virtual DOM tree by calling the component's render function.
2. **Diffs** the new tree against the previous one (reconciliation) to find what changed.
3. **Patches** only the changed nodes into the real DOM (commit phase).

This process is called **reconciliation** and it keeps DOM mutations minimal, because touching the real DOM is significantly more expensive than comparing JavaScript objects.

React does not re-render the whole page on every state change — only the subtree that depends on the changed state is re-evaluated.

```jsx
// When count changes, React re-renders Counter,
// computes the minimal DOM update, and applies only that.
function Counter() {
  const [count, setCount] = React.useState(0);
  return <button onClick={() => setCount((c) => c + 1)}>{count}</button>;
}
```

**Important:** the VDOM is an implementation detail. React Native, for example, uses React's reconciler without a browser DOM at all.

## 🧠 Question 3

**ID**: react-003
**Title**: What is JSX and how does it work under the hood?
**Difficulty**: Easy
**Category**: JSX & Rendering

### Answer 📄

JSX (JavaScript XML) is a syntax extension that lets you write HTML-like markup inside JavaScript. It is not valid JavaScript on its own — it must be compiled by a transpiler (Babel or the TypeScript compiler) before the browser can run it.

Each JSX element compiles to a `React.createElement()` call (classic runtime) or a `jsx()` call from `react/jsx-runtime` (automatic runtime, React 17+):

```jsx
// JSX
const element = <h1 className="title">Hello, {name}</h1>;

// Compiled (automatic runtime — React 17+)
import { jsx as _jsx } from 'react/jsx-runtime';
const element = _jsx('h1', { className: 'title', children: `Hello, ${name}` });
```

The result is a plain JavaScript object — a **React element** (vnode):

```js
{
  type: 'h1',
  props: { className: 'title', children: 'Hello, Alice' },
  key: null,
  ref: null,
}
```

**Key JSX rules:**

- A component must return a single root element (use `<>...</>` fragments for multiple roots).
- `class` becomes `className`; `for` becomes `htmlFor`.
- All tags must be closed: `<img />`, `<br />`.
- JavaScript expressions go inside `{}`.
- Component names must start with a capital letter to distinguish from HTML tags.

## 🧠 Question 4

**ID**: react-004
**Title**: What are functional components in React?
**Difficulty**: Easy
**Category**: Components

### Answer 📄

A functional component is a JavaScript function that accepts a `props` object and returns JSX (React elements). It is the standard way to write components in modern React.

```jsx
function Greeting({ name, role = 'user' }) {
  return (
    <div>
      <h1>Hello, {name}!</h1>
      <p>Role: {role}</p>
    </div>
  );
}

// Arrow function syntax — equally valid
const Greeting = ({ name, role = 'user' }) => (
  <div>
    <h1>Hello, {name}!</h1>
    <p>Role: {role}</p>
  </div>
);
```

Before React 16.8, functional components were "stateless" — state and lifecycle required class components. Hooks changed this: functional components can now use state (`useState`), side effects (`useEffect`), context, refs, and any custom hook.

**Why functional components are preferred:**

- Simpler mental model — no `this`, no lifecycle method naming conventions.
- Easier to test — pure functions are predictable.
- Better TypeScript inference.
- All React features (Concurrent Mode, Server Components) are designed around functions.

Class components still work but are no longer the recommended approach.

## 🧠 Question 5

**ID**: react-005
**Title**: What are props in React and how do they work?
**Difficulty**: Easy
**Category**: Props & State

### Answer 📄

Props (short for "properties") are the mechanism for passing data from a parent component to a child component. They are read-only — a component must never modify its own props.

```jsx
// Parent passes data via props
function App() {
  return <UserCard name="Alice" age={30} isAdmin={true} />;
}

// Child receives props as a plain object
function UserCard({ name, age, isAdmin }) {
  return (
    <div>
      <h2>{name}</h2>
      <p>Age: {age}</p>
      {isAdmin && <span>Admin</span>}
    </div>
  );
}
```

**Prop types:**

- Strings: `name="Alice"` (no braces needed)
- Anything else (numbers, booleans, arrays, objects, functions): `age={30}`
- Omitted boolean: `<Button disabled />` is equivalent to `disabled={true}`

**`children` prop** — content between opening and closing tags is passed as `props.children`:

```jsx
function Card({ children, title }) {
  return (
    <div className="card">
      <h3>{title}</h3>
      {children}
    </div>
  );
}

// Usage
<Card title="Info">
  <p>Some content</p>
</Card>;
```

**Spreading props** — use the spread operator to forward all props:

```jsx
function Button({ className, ...rest }) {
  return <button className={`btn ${className}`} {...rest} />;
}
```
