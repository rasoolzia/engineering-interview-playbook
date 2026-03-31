---
topic: react
language: en
version: 1.1
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

## 🧠 Question 6

**ID**: react-006
**Title**: What is state in React and how is it different from props?
**Difficulty**: Easy
**Category**: Props & State

### Answer 📄

State is mutable data managed within a component. When state changes, React re-renders the component to reflect the new state. Unlike props (owned by the parent), state is owned and controlled by the component itself.

```jsx
import { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0); // initial value: 0

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount((c) => c + 1)}>+</button>
      <button onClick={() => setCount((c) => c - 1)}>-</button>
    </div>
  );
}
```

**Props vs State:**

|                     | Props                        | State                    |
| ------------------- | ---------------------------- | ------------------------ |
| Owner               | Parent component             | The component itself     |
| Mutable?            | No (read-only)               | Yes (via setter)         |
| Triggers re-render? | Yes (when parent re-renders) | Yes (when setter called) |
| Passed via          | Function argument            | `useState` hook          |

**Functional update form** — pass a function to the setter when the new value depends on the previous value. This is essential for correctness inside async callbacks or batched updates:

```js
setCount((prev) => prev + 1); // safe — always reads latest value
setCount(count + 1); // potentially stale in concurrent mode
```

**State is local and encapsulated** — sibling components do not share state directly. To share state, lift it to the nearest common ancestor.

## 🧠 Question 7

**ID**: react-007
**Title**: How does React handle events?
**Difficulty**: Easy
**Category**: Forms & Events

### Answer 📄

React uses a **synthetic event system** that wraps the browser's native DOM events. React attaches a single event listener at the root of the React tree (not on each element), and dispatches events to the correct handlers through event delegation.

```jsx
function Form() {
  function handleSubmit(event) {
    event.preventDefault(); // works just like native preventDefault
    console.log('submitted');
  }

  function handleChange(event) {
    console.log(event.target.value); // SyntheticEvent — same API as native
  }

  return (
    <form onSubmit={handleSubmit}>
      <input onChange={handleChange} />
    </form>
  );
}
```

**Key differences from native HTML events:**

- React event names are camelCase: `onClick`, `onChange`, `onSubmit` (not `onclick`).
- You pass a function reference, not a string: `onClick={handleClick}` not `onclick="handleClick()"`.
- Synthetic events are pooled in older React (≤ 16) and reused — accessing them asynchronously required `event.persist()`. In React 17+ this pooling was removed.

**Event propagation** works the same as native events (bubbles, capture phase). You can stop propagation with `event.stopPropagation()`.

React 17 changed the root of event delegation from `document` to the React root container, which makes micro-frontend composition with multiple React versions safer.

## 🧠 Question 8

**ID**: react-008
**Title**: How does conditional rendering work in React?
**Difficulty**: Easy
**Category**: JSX & Rendering

### Answer 📄

React has no special template directives for conditionals — you use plain JavaScript expressions inside JSX.

**Ternary operator** — the most common pattern:

```jsx
function Alert({ type, message }) {
  return (
    <div className={`alert alert-${type}`}>
      {type === 'error' ? <ErrorIcon /> : <InfoIcon />}
      <span>{message}</span>
    </div>
  );
}
```

**Short-circuit `&&`** — renders the right side only when the left side is truthy:

```jsx
{
  isLoggedIn && <Dashboard />;
}
```

**Pitfall:** if the left side is `0`, React renders `0` in the DOM (because `0` is falsy but also a valid renderable value). Use `!!` or a ternary to be safe:

```jsx
{
  items.length > 0 && <List items={items} />;
} // safe — boolean
{
  items.length && <List items={items} />;
} // dangerous — renders "0" if empty
```

**Early return pattern:**

```jsx
function Profile({ user }) {
  if (!user) return <p>Loading...</p>;
  return <div>{user.name}</div>;
}
```

**`null` to render nothing:**

```jsx
function Banner({ visible, message }) {
  if (!visible) return null;
  return <div className="banner">{message}</div>;
}
```

## 🧠 Question 9

**ID**: react-009
**Title**: How do you render lists in React and why is the `key` prop important?
**Difficulty**: Easy
**Category**: JSX & Rendering

### Answer 📄

Lists in React are rendered by mapping over an array and returning JSX for each item. Each element in the list must have a unique `key` prop.

```jsx
function TodoList({ todos }) {
  return (
    <ul>
      {todos.map((todo) => (
        <li key={todo.id}>
          <span>{todo.text}</span>
          {todo.done && <span>✓</span>}
        </li>
      ))}
    </ul>
  );
}
```

**Why `key` matters:**

When React reconciles a list, it uses `key` to match elements between the previous and new render. Without stable keys, React falls back to index-based matching, which causes incorrect behavior when items are reordered, inserted, or deleted:

- Component state (like an input's typed value) gets attached to the wrong element.
- Unnecessary DOM mutations occur.
- Animations and focus are disrupted.

**Rules for keys:**

- Must be **unique among siblings** (not globally unique).
- Must be **stable** — the same item should have the same key across renders.
- Should be a **stable identifier** from your data (database ID, UUID). Avoid using array index unless the list is static and never reordered.

```jsx
// Bad — index as key breaks with sorting/filtering
{
  items.map((item, index) => <Item key={index} {...item} />);
}

// Good — stable ID from data
{
  items.map((item) => <Item key={item.id} {...item} />);
}
```

## 🧠 Question 10

**ID**: react-010
**Title**: What are controlled and uncontrolled components in React?
**Difficulty**: Easy
**Category**: Forms & Events

### Answer 📄

**Controlled components** — form elements whose value is driven by React state. The component is the single source of truth, and every keystroke goes through a state update.

```jsx
function ControlledInput() {
  const [value, setValue] = useState('');

  return (
    <input
      value={value} // React controls the value
      onChange={(e) => setValue(e.target.value)}
    />
  );
}
```

**Uncontrolled components** — form elements that manage their own internal state. React reads the value via a `ref` only when needed (e.g., on form submit).

```jsx
function UncontrolledInput() {
  const inputRef = useRef(null);

  function handleSubmit() {
    console.log(inputRef.current.value); // read on demand
  }

  return (
    <>
      <input ref={inputRef} defaultValue="initial" />
      <button onClick={handleSubmit}>Submit</button>
    </>
  );
}
```

**When to use each:**

|                                           | Controlled             | Uncontrolled            |
| ----------------------------------------- | ---------------------- | ----------------------- |
| Validation on every keystroke             | ✅ Natural             | ❌ Requires ref polling |
| Instant feedback (format, disable submit) | ✅                     | ❌                      |
| File inputs                               | ❌ Can't control value | ✅ Must use ref         |
| Simple forms, third-party integrations    | ❌ More boilerplate    | ✅ Less code            |

Most React forms use controlled components. Libraries like React Hook Form take a hybrid approach (uncontrolled under the hood for performance, controlled-like API for validation).
