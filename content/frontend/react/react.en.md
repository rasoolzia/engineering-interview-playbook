---
topic: react
language: en
version: 1.7
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

## 🧠 Question 11

**ID**: react-011
**Title**: What is a React Fragment and when should you use it?
**Difficulty**: Easy
**Category**: JSX & Rendering

### Answer 📄

A Fragment lets a component return multiple elements without adding an extra DOM node as a wrapper.

```jsx
// Without Fragment — adds an unnecessary <div>
function Columns() {
  return (
    <div>
      <td>Name</td>
      <td>Age</td>
    </div>
  ); // invalid HTML — <div> inside <tr>
}

// With Fragment — no extra DOM node
function Columns() {
  return (
    <>
      <td>Name</td>
      <td>Age</td>
    </>
  );
}
```

**Two syntaxes:**

```jsx
// Shorthand — cannot accept props
<>...</>;

// Explicit — required when you need a key (e.g., mapping a list)
function List({ items }) {
  return items.map((item) => (
    <React.Fragment key={item.id}>
      <dt>{item.term}</dt>
      <dd>{item.description}</dd>
    </React.Fragment>
  ));
}
```

**Use cases:**

- Returning multiple table cells (`<td>`) or rows (`<tr>`) from a component.
- Grouping elements returned from a component without polluting the DOM.
- Rendering a list where each item produces multiple sibling elements.

Fragments produce no DOM output, so they have no impact on styling or layout.

## 🧠 Question 12

**ID**: react-012
**Title**: What is the difference between class components and functional components?
**Difficulty**: Easy
**Category**: Components

### Answer 📄

Both types can produce the same output, but they differ significantly in syntax, API, and how they manage state and lifecycle.

**Class components** use ES6 classes, have `this`, lifecycle methods, and `this.state`:

```jsx
class Counter extends React.Component {
  state = { count: 0 };

  componentDidMount() {
    document.title = `Count: ${this.state.count}`;
  }

  componentDidUpdate() {
    document.title = `Count: ${this.state.count}`;
  }

  render() {
    return (
      <button onClick={() => this.setState((s) => ({ count: s.count + 1 }))}>
        {this.state.count}
      </button>
    );
  }
}
```

**Functional components** use hooks:

```jsx
function Counter() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    document.title = `Count: ${count}`;
  });

  return <button onClick={() => setCount((c) => c + 1)}>{count}</button>;
}
```

**Key differences:**

|                       | Class Components               | Functional Components             |
| --------------------- | ------------------------------ | --------------------------------- |
| State                 | `this.state` + `this.setState` | `useState`                        |
| Lifecycle             | `componentDidMount`, etc.      | `useEffect`                       |
| `this` binding        | Required                       | Not needed                        |
| Code reuse            | Mixins (problematic)           | Custom hooks (clean)              |
| Error boundaries      | Supported                      | Not yet (as of React 18)          |
| React future features | Not prioritized                | All new features target functions |

Class components are fully supported but are considered legacy. All new React APIs (Concurrent Mode, Server Components) are designed around functions.

## 🧠 Question 13

**ID**: react-013
**Title**: What is reconciliation in React?
**Difficulty**: Medium
**Category**: Rendering Behavior

### Answer 📄

Reconciliation is the process React uses to determine what changed in the UI between renders and update the DOM accordingly.

When state or props change, React calls the component's render function and gets a new virtual DOM tree. It then **diffs** this new tree against the previous one using a heuristic algorithm with two key assumptions:

1. **Different element types produce different trees.** If the root type changes (e.g., `<div>` → `<span>`), React tears down the entire old subtree and builds a new one from scratch — including unmounting all child components.

2. **`key` identifies stable elements across renders.** When diffing lists, React uses the `key` prop to match elements between renders. Elements with the same key are treated as the same element (updated in place); missing/new keys trigger unmount/mount.

```jsx
// React assumes the root element changed — unmounts Foo, mounts Bar
{
  condition ? <Foo /> : <Bar />;
}

// React sees same root type — updates Foo's props (more efficient)
{
  condition ? <Foo color="red" /> : <Foo color="blue" />;
}
```

**Why this matters for performance:** React's reconciler avoids expensive full-tree comparisons by applying these heuristics. The result is O(n) tree diffing rather than the naive O(n³) algorithm.

The reconciler is separate from the renderer. React DOM, React Native, and React Three Fiber all share the same reconciler but target different output environments.

## 🧠 Question 14

**ID**: react-014
**Title**: What is prop drilling and how do you solve it?
**Difficulty**: Easy
**Category**: Props & State

### Answer 📄

Prop drilling occurs when data must be passed through several layers of intermediate components that do not need the data themselves — they only pass it further down.

```jsx
// Prop drilling — theme must be threaded through App → Layout → Sidebar → Button
function App() {
  const [theme, setTheme] = useState('dark');
  return <Layout theme={theme} setTheme={setTheme} />;
}
function Layout({ theme, setTheme }) {
  return <Sidebar theme={theme} setTheme={setTheme} />;
}
function Sidebar({ theme, setTheme }) {
  return <ThemeButton theme={theme} setTheme={setTheme} />;
}
function ThemeButton({ theme, setTheme }) {
  return (
    <button onClick={() => setTheme((t) => (t === 'dark' ? 'light' : 'dark'))}>
      {theme}
    </button>
  );
}
```

**Problems it causes:**

- Intermediate components become tightly coupled to data they don't use.
- Refactoring is painful — adding a prop requires updating every layer.
- Components are harder to reuse in isolation.

**Solutions:**

1. **Context API** — provide data at a high level and consume it anywhere in the tree without threading:

```jsx
const ThemeContext = createContext('light');
// Wrap the tree: <ThemeContext.Provider value={theme}>
// Consume anywhere: const theme = useContext(ThemeContext);
```

2. **State management libraries** (Zustand, Redux, Jotai) — global store accessible from any component.

3. **Component composition** — pass components as children or props to avoid drilling data:

```jsx
function Layout({ children }) {
  return <div>{children}</div>;
}
// The parent controls what goes inside, so no drilling needed
```

## 🧠 Question 15

**ID**: react-015
**Title**: What is the `StrictMode` component and what does it do?
**Difficulty**: Medium
**Category**: React Basics

### Answer 📄

`<React.StrictMode>` is a development-only wrapper that activates additional warnings and behaviors to help you identify potential issues in your application.

```jsx
import { StrictMode } from 'react';
import { createRoot } from 'react-dom/client';

createRoot(document.getElementById('root')).render(
  <StrictMode>
    <App />
  </StrictMode>,
);
```

**What StrictMode does (development only — no production impact):**

1. **Double-invokes render functions, state initializers, and reducers** — to detect side effects in functions that should be pure. If your component has accidental side effects (e.g., incrementing a counter in render), they become visible.

2. **Mounts → unmounts → remounts every component once** (React 18+) — to verify that effects have proper cleanup. This simulates what happens when components are preserved/restored (e.g., navigating back in a React Native screen or future tab-suspend behavior).

3. **Warns about deprecated APIs** — legacy lifecycle methods (`componentWillMount`, etc.), legacy string refs, `findDOMNode`, etc.

4. **Detects accidental mutations of state** — helps surface bugs where state is mutated directly.

StrictMode applies to the component subtree it wraps, so you can enable it selectively for specific parts of the app.

## 🧠 Question 16

**ID**: react-016
**Title**: What is `React.memo` and when does it help?
**Difficulty**: Medium
**Category**: Performance Optimization

### Answer 📄

`React.memo` is a higher-order component that memoizes a functional component's render output. If the component's props have not changed (using shallow equality), React skips re-rendering and reuses the last rendered output.

```jsx
const UserCard = React.memo(function UserCard({ name, age }) {
  console.log('rendering UserCard');
  return (
    <div>
      {name} — {age}
    </div>
  );
});

// If parent re-renders but name and age haven't changed,
// UserCard is NOT re-rendered.
```

**When it helps:**

- The parent re-renders frequently (e.g., it manages a fast-changing state that the child doesn't use).
- The component is expensive to render (complex computations or many child nodes).
- The component receives stable props (primitives or memoized objects/functions).

**When it does NOT help (or hurts):**

- Props change on every render anyway — the shallow comparison adds overhead with no benefit.
- Props are objects or functions created inline in the parent — a new reference fails the equality check:

```jsx
// This breaks memo — new object reference on every parent render
<UserCard style={{ color: 'red' }} onClick={() => doSomething()} />;

// Fix: memoize objects and functions in the parent
const style = useMemo(() => ({ color: 'red' }), []);
const handleClick = useCallback(() => doSomething(), []);
<UserCard style={style} onClick={handleClick} />;
```

**Custom comparison** — pass a second argument for fine-grained control:

```jsx
React.memo(MyComponent, (prevProps, nextProps) => {
  return prevProps.id === nextProps.id; // true = skip re-render
});
```

## 🧠 Question 17

**ID**: react-017
**Title**: What is the `useEffect` hook and how does the dependency array work?
**Difficulty**: Medium
**Category**: Effects & Lifecycle

### Answer 📄

`useEffect` lets you synchronize a component with an external system (DOM API, network request, subscription, timer) after React has committed the render to the DOM.

```jsx
useEffect(() => {
  // Side effect — runs after every render by default
  document.title = `You clicked ${count} times`;
});
```

**Dependency array controls when the effect runs:**

```jsx
// No dependency array — runs after EVERY render
useEffect(() => { ... });

// Empty array — runs ONCE after the initial mount only
useEffect(() => { ... }, []);

// With dependencies — runs after mount AND whenever count or userId changes
useEffect(() => {
  fetchUser(userId);
}, [userId]);
```

**Cleanup function** — returned from the effect. Runs before the effect re-runs and when the component unmounts:

```jsx
useEffect(() => {
  const subscription = subscribe(userId, onMessage);
  return () => subscription.unsubscribe(); // cleanup
}, [userId]);
```

**React 18 + StrictMode** — effects are mounted, cleaned up, and remounted once in development to surface cleanup bugs. This is intentional.

**Rules:**

- Never conditionally call `useEffect` — hooks must be called in the same order every render.
- Include all values read inside the effect in the dependency array (enforced by the `react-hooks/exhaustive-deps` ESLint rule).
- Do not use `useEffect` for event handlers — those belong directly on elements.

## 🧠 Question 18

**ID**: react-018
**Title**: What is `useState` and how does state updating work?
**Difficulty**: Easy
**Category**: Hooks

### Answer 📄

`useState` is the fundamental hook for adding local state to a functional component. It returns a pair: the current state value and a setter function.

```jsx
const [state, setState] = useState(initialValue);
```

**State updates are asynchronous and batched** — calling `setState` does not immediately change `state`. React schedules a re-render and applies all state updates from the same event handler in a single batch:

```jsx
function handleClick() {
  setCount((c) => c + 1);
  setCount((c) => c + 1);
  // React batches these — count increases by 2 after one re-render
}
```

**Functional update form** — pass a function when the new value depends on the previous:

```jsx
setState((prev) => ({ ...prev, name: 'Alice' }));
```

Always use this form when updating inside async callbacks, `useEffect`, or event handlers where the state value may be stale.

**State initialization** — for expensive computations, pass a function to avoid running it on every render:

```jsx
// Bad — runs expensiveCalc() on every render even though only used once
const [value, setValue] = useState(expensiveCalc());

// Good — runs once on initial mount only
const [value, setValue] = useState(() => expensiveCalc());
```

**Objects and arrays** — React does not merge object state automatically (unlike `this.setState` in class components). You must spread manually:

```jsx
setState((prev) => ({ ...prev, age: 31 })); // correct
setState({ age: 31 }); // wrong — discards other fields
```

## 🧠 Question 19

**ID**: react-019
**Title**: What is `useRef` and when should you use it?
**Difficulty**: Medium
**Category**: Hooks

### Answer 📄

`useRef` returns a mutable `ref` object with a `.current` property that persists across renders without triggering a re-render when changed. It has two primary use cases.

**1. Accessing DOM elements directly:**

```jsx
function AutoFocusInput() {
  const inputRef = useRef(null);

  useEffect(() => {
    inputRef.current.focus();
  }, []);

  return <input ref={inputRef} />;
}
```

**2. Storing mutable values that should NOT trigger re-renders:**

```jsx
function Timer() {
  const intervalId = useRef(null);
  const [seconds, setSeconds] = useState(0);

  function start() {
    intervalId.current = setInterval(() => {
      setSeconds((s) => s + 1);
    }, 1000);
  }

  function stop() {
    clearInterval(intervalId.current);
  }

  return (
    <>
      <p>{seconds}s</p>
      <button onClick={start}>Start</button>
      <button onClick={stop}>Stop</button>
    </>
  );
}
```

**Key characteristics:**

- Changing `ref.current` does **not** trigger a re-render — unlike `useState`.
- The ref object is the same object across all renders (referentially stable).
- Useful for: storing previous values, animation frame IDs, WebSocket instances, canvas contexts.

**`useRef` vs `useState`:**

|                                | `useRef`                    | `useState` |
| ------------------------------ | --------------------------- | ---------- |
| Triggers re-render?            | No                          | Yes        |
| Value persists across renders? | Yes                         | Yes        |
| Access                         | `.current`                  | Direct     |
| Use for                        | DOM access, mutable storage | UI state   |

## 🧠 Question 20

**ID**: react-020
**Title**: What is `useMemo` and when should you use it?
**Difficulty**: Medium
**Category**: Performance Optimization

### Answer 📄

`useMemo` memoizes the result of an expensive computation, recomputing it only when one of its dependencies changes.

```jsx
const expensiveValue = useMemo(() => {
  return computeExpensiveValue(a, b);
}, [a, b]);
```

React skips the computation on re-renders where `a` and `b` have not changed, returning the cached result instead.

**When to use `useMemo`:**

1. **Expensive computations** — sorting, filtering, or transforming large datasets:

```jsx
const sortedUsers = useMemo(
  () => [...users].sort((a, b) => a.name.localeCompare(b.name)),
  [users],
);
```

2. **Stable object/array references for child components wrapped in `React.memo`** or used in `useEffect` dependency arrays:

```jsx
const config = useMemo(() => ({ theme, locale }), [theme, locale]);
// config reference is stable — won't re-trigger effects or memo checks
```

**When NOT to use `useMemo`:**

- For cheap calculations — the memoization overhead can exceed the savings.
- When dependencies change on every render anyway — the cache is never used.
- As a premature optimization — profile first.

**`useMemo` vs `useCallback`:**

```jsx
useMemo(() => fn(), [deps]); // memoizes the RETURN VALUE of fn
useCallback(fn, [deps]); // memoizes the FUNCTION fn itself
```

React may choose to discard cached `useMemo` values (e.g., under memory pressure) — do not rely on `useMemo` for correctness, only performance.

## 🧠 Question 21

**ID**: react-021
**Title**: What is `useCallback` and when should you use it?
**Difficulty**: Medium
**Category**: Performance Optimization

### Answer 📄

`useCallback` returns a memoized version of a callback function. The function identity is preserved across renders as long as its dependencies do not change.

```jsx
const handleClick = useCallback(() => {
  doSomething(id);
}, [id]);
```

Without `useCallback`, a new function reference is created on every render, which can cause problems when passed to:

- Child components wrapped in `React.memo` (breaks the shallow prop comparison).
- `useEffect` dependency arrays (triggers the effect unnecessarily).

**Practical example:**

```jsx
const MemoizedChild = React.memo(function Child({ onAction }) {
  console.log('Child rendered');
  return <button onClick={onAction}>Action</button>;
});

function Parent() {
  const [count, setCount] = useState(0);

  // Without useCallback: new function on every render → Child always re-renders
  const handleAction = useCallback(() => {
    console.log('action');
  }, []); // stable reference — Child only renders once

  return (
    <>
      <button onClick={() => setCount((c) => c + 1)}>Count: {count}</button>
      <MemoizedChild onAction={handleAction} />
    </>
  );
}
```

**`useCallback(fn, deps)` is equivalent to `useMemo(() => fn, deps)`.**

**When NOT to use it:**

- When the child isn't wrapped in `React.memo` — no benefit.
- When the function is not passed to anything that depends on referential stability.
- Premature optimization — profile before applying.

## 🧠 Question 22

**ID**: react-022
**Title**: What are the rules of hooks?
**Difficulty**: Medium
**Category**: Hooks

### Answer 📄

React enforces two fundamental rules for hooks to ensure they work correctly.

**Rule 1: Only call hooks at the top level.**

Never call hooks inside conditionals, loops, or nested functions. React relies on the order of hook calls being the same on every render to correctly associate each hook with its state slot.

```jsx
// ❌ Wrong — hook inside a condition
function Component({ isLoggedIn }) {
  if (isLoggedIn) {
    const [user, setUser] = useState(null); // breaks hook order
  }
}

// ✅ Correct — condition inside the hook's usage
function Component({ isLoggedIn }) {
  const [user, setUser] = useState(null);
  if (!isLoggedIn) return null;
  // use user...
}
```

**Rule 2: Only call hooks from React functions.**

Hooks must be called from:

- Functional components
- Custom hooks

Never from regular JavaScript functions, class components, or event handlers directly.

**Why these rules exist:**

React internally maintains a linked list of hook states for each component, indexed by call order. If a hook is conditionally called, the order changes between renders, causing React to read the wrong state slot — leading to bugs that are very hard to debug.

The `eslint-plugin-react-hooks` package enforces both rules automatically during development.

## 🧠 Question 23

**ID**: react-023
**Title**: What are custom hooks and how do you write them?
**Difficulty**: Medium
**Category**: Hooks

### Answer 📄

A custom hook is a JavaScript function whose name starts with `use` that can call other hooks. Custom hooks are the primary mechanism for extracting and sharing stateful logic between components — replacing mixins and render props for this purpose.

```jsx
// useLocalStorage — persists state to localStorage
function useLocalStorage(key, initialValue) {
  const [storedValue, setStoredValue] = useState(() => {
    try {
      const item = window.localStorage.getItem(key);
      return item ? JSON.parse(item) : initialValue;
    } catch {
      return initialValue;
    }
  });

  const setValue = useCallback(
    (value) => {
      try {
        const valueToStore =
          value instanceof Function ? value(storedValue) : value;
        setStoredValue(valueToStore);
        window.localStorage.setItem(key, JSON.stringify(valueToStore));
      } catch (error) {
        console.error(error);
      }
    },
    [key, storedValue],
  );

  return [storedValue, setValue];
}

// Usage — same API as useState
function App() {
  const [theme, setTheme] = useLocalStorage('theme', 'light');
  return (
    <button onClick={() => setTheme((t) => (t === 'light' ? 'dark' : 'light'))}>
      {theme}
    </button>
  );
}
```

**Best practices:**

- Always prefix with `use` — this is what allows the ESLint hook rules to lint them correctly.
- Return values that mirror the pattern of the hooks they wrap (tuple `[value, setter]` or an object).
- A custom hook should have a single, focused responsibility.
- Accept inputs as arguments instead of hardcoding values to make the hook reusable.
- Keep hook logic independent of rendering (no JSX inside hooks).

## 🧠 Question 24

**ID**: react-024
**Title**: What is the Context API and how do you use it?
**Difficulty**: Medium
**Category**: Context API

### Answer 📄

The Context API provides a way to pass data through the component tree without prop drilling. It creates a "broadcast channel" that any descendant component can subscribe to.

**Creating and providing context:**

```jsx
import { createContext, useContext, useState } from 'react';

const ThemeContext = createContext('light'); // 'light' is the default value

function ThemeProvider({ children }) {
  const [theme, setTheme] = useState('light');

  return (
    <ThemeContext.Provider value={{ theme, setTheme }}>
      {children}
    </ThemeContext.Provider>
  );
}
```

**Consuming context with `useContext`:**

```jsx
function ThemeButton() {
  const { theme, setTheme } = useContext(ThemeContext);

  return (
    <button onClick={() => setTheme((t) => (t === 'light' ? 'dark' : 'light'))}>
      Current: {theme}
    </button>
  );
}

// In the app
function App() {
  return (
    <ThemeProvider>
      <ThemeButton />
    </ThemeProvider>
  );
}
```

**Performance consideration** — every consumer of a context re-renders when the context value changes. If the context value is an object created inline, it changes on every provider re-render:

```jsx
// Bad — new object on every render → all consumers re-render
<Context.Provider value={{ theme, setTheme }}>

// Better — memoize the value
const value = useMemo(() => ({ theme, setTheme }), [theme]);
<Context.Provider value={value}>
```

For large applications with frequently changing state, prefer a dedicated state management library over Context for performance-sensitive data.

## 🧠 Question 25

**ID**: react-025
**Title**: What is `useReducer` and when should you use it instead of `useState`?
**Difficulty**: Medium
**Category**: Hooks

### Answer 📄

`useReducer` is an alternative to `useState` for managing complex state logic. It is modelled after the Redux pattern: a reducer function receives the current state and an action and returns the next state.

```jsx
import { useReducer } from 'react';

const initialState = { count: 0, step: 1 };

function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return { ...state, count: state.count + state.step };
    case 'decrement':
      return { ...state, count: state.count - state.step };
    case 'setStep':
      return { ...state, step: action.payload };
    case 'reset':
      return initialState;
    default:
      throw new Error(`Unknown action: ${action.type}`);
  }
}

function Counter() {
  const [state, dispatch] = useReducer(reducer, initialState);

  return (
    <div>
      <p>
        Count: {state.count} (step: {state.step})
      </p>
      <button onClick={() => dispatch({ type: 'increment' })}>+</button>
      <button onClick={() => dispatch({ type: 'decrement' })}>-</button>
      <button onClick={() => dispatch({ type: 'reset' })}>Reset</button>
    </div>
  );
}
```

**When to prefer `useReducer` over `useState`:**

- State has multiple sub-values that change together.
- Next state depends on the previous state in complex ways.
- The update logic is complex enough that it benefits from a pure, testable reducer function.
- You want to centralize all state transitions in one place.
- You're passing `dispatch` down to children and want action-based updates to stay explicit and centralized.

**`useReducer` vs Redux:** `useReducer` is local to the component (or shared via Context). Redux is a global store with middleware, DevTools, and time-travel debugging.

## 🧠 Question 26

**ID**: react-026
**Title**: What is `useLayoutEffect` and how does it differ from `useEffect`?
**Difficulty**: Hard
**Category**: Effects & Lifecycle

### Answer 📄

Both hooks take the same signature, but they fire at different times in the rendering cycle.

**`useEffect`** — runs asynchronously **after** the browser has painted the screen. The component renders, the browser updates the visual output, and then the effect runs.

**`useLayoutEffect`** — runs synchronously **after** React has computed the DOM mutations but **before** the browser paints. It blocks the paint until the effect finishes.

```
React renders → React commits DOM mutations
  → useLayoutEffect runs (synchronously)
  → Browser paints
  → useEffect runs (asynchronously)
```

**When to use `useLayoutEffect`:**

- Reading DOM measurements (scroll position, element dimensions) before the user sees the screen, to avoid a visible flicker or "flash of wrong content":

```jsx
function Tooltip({ targetRef, content }) {
  const tooltipRef = useRef(null);

  useLayoutEffect(() => {
    const targetRect = targetRef.current.getBoundingClientRect();
    const tooltip = tooltipRef.current;
    // Position tooltip before the browser paints — no flicker
    tooltip.style.top = `${targetRect.bottom}px`;
    tooltip.style.left = `${targetRect.left}px`;
  });

  return (
    <div ref={tooltipRef} className="tooltip">
      {content}
    </div>
  );
}
```

**When to stick with `useEffect`:**

- Anything that doesn't need to block painting: data fetching, subscriptions, analytics, logging.

**Server-side rendering caveat:** `useLayoutEffect` does not run on the server (there is no DOM), which causes a warning. Use `useEffect` for SSR-compatible components, or conditionally guard with `typeof window !== 'undefined'`.

## 🧠 Question 27

**ID**: react-027
**Title**: What are Error Boundaries in React?
**Difficulty**: Medium
**Category**: Components

### Answer 📄

An Error Boundary is a class component that catches JavaScript errors anywhere in its child component tree and displays a fallback UI instead of crashing the whole application.

Error boundaries catch errors during:

- Rendering
- Lifecycle methods
- Constructors of child components

They do **not** catch errors in:

- Event handlers (use try/catch)
- Asynchronous code (`setTimeout`, promises)
- Server-side rendering
- Errors in the error boundary itself

```jsx
class ErrorBoundary extends React.Component {
  state = { hasError: false, error: null };

  static getDerivedStateFromError(error) {
    // Update state to show fallback UI
    return { hasError: true, error };
  }

  componentDidCatch(error, info) {
    // Log to error reporting service
    logError(error, info.componentStack);
  }

  render() {
    if (this.state.hasError) {
      return this.props.fallback ?? <h2>Something went wrong.</h2>;
    }
    return this.props.children;
  }
}

// Usage
<ErrorBoundary fallback={<ErrorPage />}>
  <Dashboard />
</ErrorBoundary>;
```

Error boundaries themselves are still class components in React. In function-component-heavy codebases, many teams use the `react-error-boundary` package to get a reusable wrapper and hooks-friendly integration.

Wrap distinct sections of the UI in separate Error Boundaries so a crash in one section does not take down the entire application.

## 🧠 Question 28

**ID**: react-028
**Title**: What are Portals in React?
**Difficulty**: Medium
**Category**: Components

### Answer 📄

A Portal renders a component's children into a different DOM node than the component's parent — while keeping the component in its normal position in the React component tree.

```jsx
import { createPortal } from 'react-dom';

function Modal({ isOpen, onClose, children }) {
  if (!isOpen) return null;

  return createPortal(
    <div className="modal-overlay" onClick={onClose}>
      <div className="modal-content" onClick={(e) => e.stopPropagation()}>
        {children}
      </div>
    </div>,
    document.body, // render into document.body, not the parent DOM node
  );
}
```

**Why Portals exist:**

CSS properties like `overflow: hidden`, `z-index`, and `transform` on ancestor elements can clip or incorrectly stack UI that needs to visually "escape" the parent — modals, tooltips, dropdowns, and notifications.

**Key behaviors:**

- **React tree, not DOM tree** — event bubbling follows the React component hierarchy, not the DOM hierarchy. A click inside a portal bubbles up through React ancestors even though the DOM ancestors are different.
- **Context works** — the portal component can still consume context from its React parent.
- **Lifecycle is tied to the React parent** — when the parent unmounts, the portal content is also cleaned up.

```jsx
// Portal content is rendered in document.body in the DOM
// but event bubbling goes through <Page> → <App> in React
function App() {
  return (
    <Page>
      <Modal>
        {' '}
        {/* React parent is Page, DOM parent is body */}
        <button onClick={handleClose}>Close</button>
      </Modal>
    </Page>
  );
}
```

## 🧠 Question 29

**ID**: react-029
**Title**: What is `useImperativeHandle` and when do you need `forwardRef`?
**Difficulty**: Hard
**Category**: Hooks

### Answer 📄

`forwardRef` is a wrapper that lets a parent component pass a `ref` through to a child component's DOM element or a custom imperative handle.

By default, `ref` on a functional component does not work — refs can only be attached to DOM elements. `forwardRef` enables attaching refs to functional components.

```jsx
const FancyInput = forwardRef(function FancyInput(props, ref) {
  return <input ref={ref} className="fancy-input" {...props} />;
});

// Parent
function Form() {
  const inputRef = useRef(null);

  useEffect(() => {
    inputRef.current.focus(); // direct DOM access
  }, []);

  return <FancyInput ref={inputRef} />;
}
```

**`useImperativeHandle`** customizes what the parent sees through the ref — instead of the raw DOM element, the parent gets a controlled API:

```jsx
const VideoPlayer = forwardRef(function VideoPlayer(props, ref) {
  const videoRef = useRef(null);

  useImperativeHandle(ref, () => ({
    play() {
      videoRef.current.play();
    },
    pause() {
      videoRef.current.pause();
    },
    seek(time) {
      videoRef.current.currentTime = time;
    },
    // The raw videoRef.current (with its full DOM API) is NOT exposed
  }));

  return <video ref={videoRef} src={props.src} />;
});

// Parent only sees { play, pause, seek }
playerRef.current.play();
```

**When to use:** use sparingly. Exposing an imperative API is generally an anti-pattern in React's declarative model. Prefer passing state and callbacks via props. Use `useImperativeHandle` when the parent truly needs to trigger actions imperatively — focus management, media playback, animations.

## 🧠 Question 30

**ID**: react-030
**Title**: What is `React.lazy` and how does it work with `Suspense`?
**Difficulty**: Medium
**Category**: Performance Optimization

### Answer 📄

`React.lazy` enables code splitting at the component level. It wraps a dynamic `import()` and returns a lazy component that React loads only when it is first rendered.

```jsx
import { lazy, Suspense } from 'react';

// The component bundle is only downloaded when Dashboard is rendered
const Dashboard = lazy(() => import('./Dashboard'));
const Settings = lazy(() => import('./Settings'));

function App() {
  const [page, setPage] = useState('dashboard');

  return (
    <Suspense fallback={<LoadingSpinner />}>
      {page === 'dashboard' ? <Dashboard /> : <Settings />}
    </Suspense>
  );
}
```

**How it works:**

1. `React.lazy(() => import('./Dashboard'))` creates a component that holds a Promise.
2. When React tries to render the lazy component for the first time, it reads the Promise.
3. If the Promise is pending, React "throws" the Promise — `<Suspense>` catches it and shows the fallback.
4. Once the Promise resolves (chunk downloaded), React re-renders the component.

**Requirements:**

- The dynamic import must resolve to a module with a **default export** that is a React component.
- A `<Suspense>` boundary must exist somewhere above the lazy component in the tree.

**Combining with React Router** for route-level splitting:

```jsx
const Home = lazy(() => import('./pages/Home'));
const About = lazy(() => import('./pages/About'));

<Routes>
  <Route
    path="/"
    element={
      <Suspense fallback={<Spinner />}>
        <Home />
      </Suspense>
    }
  />
  <Route
    path="/about"
    element={
      <Suspense fallback={<Spinner />}>
        <About />
      </Suspense>
    }
  />
</Routes>;
```

## 🧠 Question 31

**ID**: react-031
**Title**: How does React batch state updates?
**Difficulty**: Hard
**Category**: Rendering Behavior

### Answer 📄

Batching is React's optimization of grouping multiple state updates from the same event into a single re-render.

**React 17 and earlier:** only batched updates inside React event handlers. Updates inside `setTimeout`, `Promise.then`, or native event listeners were NOT batched — each triggered a separate re-render.

**React 18:** introduced **Automatic Batching** — ALL state updates, regardless of where they originate, are batched by default:

```jsx
// React 18 — all three updates batched into ONE re-render
setTimeout(() => {
  setCount((c) => c + 1);
  setFlag((f) => !f);
  setData((d) => [...d, 1]);
  // Only ONE re-render happens
}, 1000);

// Also batched inside Promise.then, native event listeners, etc.
fetch('/api').then(() => {
  setLoading(false);
  setData(result);
  // ONE re-render
});
```

**Opting out of batching with `flushSync`:**

```jsx
import { flushSync } from 'react-dom';

function handleClick() {
  flushSync(() => {
    setCount((c) => c + 1); // triggers immediate re-render
  });
  // DOM is updated here — useful for reading DOM measurements between updates
  flushSync(() => {
    setFlag((f) => !f);
  });
}
```

Use `flushSync` sparingly — it forces synchronous rendering which reduces performance and can cause issues with Concurrent Mode features.

## 🧠 Question 32

**ID**: react-032
**Title**: What is `useTransition` and when should you use it?
**Difficulty**: Hard
**Category**: Concurrent React

### Answer 📄

`useTransition` is a Concurrent React hook that marks a state update as "non-urgent" (a transition). React keeps the UI responsive during the transition, deferring the expensive update if a higher-priority update (like a keystroke) comes in.

```jsx
import { useTransition, useState } from 'react';

function SearchPage() {
  const [query, setQuery] = useState('');
  const [results, setResults] = useState([]);
  const [isPending, startTransition] = useTransition();

  function handleChange(e) {
    setQuery(e.target.value); // urgent — updates input immediately

    startTransition(() => {
      // Non-urgent — React may defer this and keep the input responsive
      setResults(searchDatabase(e.target.value));
    });
  }

  return (
    <>
      <input value={query} onChange={handleChange} />
      {isPending && <Spinner />}
      <ResultsList results={results} />
    </>
  );
}
```

**How it works internally:**

- React renders the transition update at a lower priority.
- If a new urgent update (e.g., another keystroke) arrives before the transition finishes, React discards the in-progress transition render and starts fresh.
- `isPending` is `true` while the transition is in progress — use it to show loading indicators.

**`useTransition` vs `useDeferredValue`:**

- `useTransition` wraps a state setter — you control which update is deferred.
- `useDeferredValue` wraps a value — useful when you receive the value from a prop or another component and can't control the update timing.

## 🧠 Question 33

**ID**: react-033
**Title**: What is `useDeferredValue` and how does it differ from debouncing?
**Difficulty**: Hard
**Category**: Concurrent React

### Answer 📄

`useDeferredValue` accepts a value and returns a deferred version of it. During a re-render, if there is a higher-priority update pending, the deferred value lags behind — React reuses the old value to keep the UI responsive and re-renders with the new value when the browser is idle.

```jsx
import { useDeferredValue, memo } from 'react';

function SearchPage({ query }) {
  const deferredQuery = useDeferredValue(query);

  return (
    <>
      <p>Showing results for: {query}</p> {/* always current */}
      <Results query={deferredQuery} /> {/* may lag behind */}
    </>
  );
}

// Wrap the expensive component in memo so it only re-renders
// when deferredQuery actually changes
const Results = memo(function Results({ query }) {
  // Expensive computation / rendering
  const items = searchItems(query);
  return (
    <ul>
      {items.map((i) => (
        <li key={i.id}>{i.name}</li>
      ))}
    </ul>
  );
});
```

**Difference from debouncing:**

- **Debouncing** delays the update by a fixed timer — always introduces latency, even on fast devices.
- **`useDeferredValue`** is adaptive — on fast devices with no competing updates, it renders immediately. The deferral only kicks in when there is contention.

**Difference from `useTransition`:**

- `useTransition` wraps the state setter — use when you control where the state update happens.
- `useDeferredValue` wraps the received value — use when you receive a value as a prop or from a context and cannot control when it updates.

## 🧠 Question 34

**ID**: react-034
**Title**: What are React Server Components?
**Difficulty**: Hard
**Category**: Server Components

### Answer 📄

React Server Components (RSC) are components that render exclusively on the server and are never sent to the client as JavaScript. They can directly access server-side resources (databases, file systems, internal APIs) without API round trips.

**Key properties:**

- Zero JavaScript bundle impact — their code never reaches the browser.
- Can use `async/await` directly in the component body.
- Cannot use state (`useState`), effects (`useEffect`), or browser-only APIs.
- Cannot handle user interactions directly.

```jsx
// app/users/page.jsx (Next.js App Router)
// This component runs ONLY on the server — no JS sent to client

async function UsersPage() {
  // Direct database access — no API fetch needed
  const users = await db.query('SELECT * FROM users');

  return (
    <ul>
      {users.map((user) => (
        <li key={user.id}>
          <UserCard user={user} /> {/* also a server component */}
          <InteractiveButton userId={user.id} /> {/* client component */}
        </li>
      ))}
    </ul>
  );
}
```

**Server Components vs Client Components:**

|                          | Server Components | Client Components         |
| ------------------------ | ----------------- | ------------------------- |
| Renders on               | Server only       | Server (initial) + Client |
| Bundle size              | Zero              | Added to JS bundle        |
| State/Effects            | ❌                | ✅                        |
| Direct DB/FS access      | ✅                | ❌                        |
| `async/await` in body    | ✅                | ❌                        |
| `"use client"` directive | Not needed        | Required                  |

**The interleaving model** — server and client components can be nested. A server component can import client components, but a client component cannot import a server component (it can receive server components as children via props).

## 🧠 Question 35

**ID**: react-035
**Title**: What is hydration in React SSR and what causes hydration mismatches?
**Difficulty**: Hard
**Category**: SSR / Hydration

### Answer 📄

**Server-Side Rendering (SSR)** generates the full HTML on the server and sends it to the browser. The browser can display it immediately without waiting for JavaScript.

**Hydration** is the process where React "takes over" the server-rendered HTML on the client — attaching event listeners and making the static HTML interactive. React re-renders the component tree and reconciles it with the existing DOM instead of creating nodes from scratch.

```jsx
// Server: renders to HTML string
// Client: hydrates the existing DOM
import { hydrateRoot } from 'react-dom/client';

hydrateRoot(document.getElementById('root'), <App />);
```

**Hydration mismatches** occur when the HTML the server produces differs from what React renders on the client. React logs a warning and falls back to client-side re-rendering for the mismatched subtree.

**Common causes:**

1. **Non-deterministic rendering** — `Date.now()`, `Math.random()`, `new Date()` produce different values server vs client.
2. **Browser-only APIs** — `window`, `localStorage`, `navigator` used during render (they don't exist on the server).
3. **Conditional rendering based on `typeof window`** — renders different content server vs client.
4. **Invalid HTML** — a `<p>` inside another `<p>` which browsers auto-correct differently.
5. **Third-party browser extensions** — inject DOM nodes that React doesn't expect.

**Fixes:**

```jsx
// Guard browser APIs with useEffect or client-only rendering
const [isMounted, setIsMounted] = useState(false);
useEffect(() => setIsMounted(true), []);

return isMounted ? <ClientOnlyComponent /> : null;

// Or use suppressHydrationWarning for intentional differences
<time suppressHydrationWarning>{new Date().toLocaleString()}</time>;
```

## 🧠 Question 36

**ID**: react-036
**Title**: What is React Fiber?
**Difficulty**: Hard
**Category**: React Internals

### Answer 📄

React Fiber is the complete rewrite of React's core reconciliation algorithm, introduced in React 16. It replaced the old synchronous "stack reconciler" with an incremental, interruptible architecture.

**The problem with the old reconciler:**

The original React reconciler used a recursive tree traversal that could not be paused. Once React started rendering a large tree, it had to finish — blocking the main thread and causing dropped frames and unresponsive UI.

**What Fiber enables:**

1. **Incremental rendering** — break rendering work into small units ("fibers"). React can pause after each unit, yield to the browser (paint, handle events), and resume.
2. **Priority scheduling** — assign different priorities to different updates. A typing animation is higher priority than a background data refetch.
3. **Concurrent rendering** — work on multiple versions of the UI simultaneously (Concurrent Mode).
4. **Suspense** — "pause" rendering when data is not ready and resume when it is.

**What a Fiber is:**

A Fiber is a JavaScript object representing a unit of work for one component instance. It contains:

- Component type, props, and state
- References to parent, sibling, and child fibers (a linked list, not a tree)
- Effect flags describing what DOM mutations to make

```
FiberNode {
  type: Counter,
  stateNode: { count: 0 },
  return: <parentFiber>,
  child: <childFiber>,
  sibling: <siblingFiber>,
  effectTag: UPDATE,
  ...
}
```

React maintains two Fiber trees: the **current tree** (what is on screen) and the **work-in-progress tree** (being built). When work completes, React swaps them — this is the "double buffering" commit.

## 🧠 Question 37

**ID**: react-037
**Title**: What is the difference between the render phase and the commit phase in React?
**Difficulty**: Hard
**Category**: React Internals

### Answer 📄

React's update cycle is divided into two distinct phases with different characteristics.

**Render Phase (Reconciliation)**

- React calls component functions and builds a new virtual DOM tree.
- React diffs the new tree against the current tree to determine what changed.
- **Asynchronous and interruptible** — React can pause, abort, or restart this work. It may call component functions multiple times (this is why component functions must be pure — no side effects in render).
- No DOM mutations happen here.
- `useState`, `useMemo`, `useReducer`, and `useCallback` operate here.

**Commit Phase**

- React applies the computed changes to the real DOM.
- **Synchronous and uninterruptible** — React processes all mutations in one shot to avoid partial UI states.
- Three sub-phases:
  1. **Before mutation** — `getSnapshotBeforeUpdate` (class), reads DOM before changes.
  2. **Mutation** — insert, update, and delete DOM nodes.
  3. **Layout** — `useLayoutEffect` and `componentDidMount/Update` run synchronously here.
- After the browser paints, `useEffect` cleanup and setup run.

```
Render Phase (interruptible):
  → Component functions called
  → Virtual DOM diffed

Commit Phase (synchronous):
  → DOM mutations applied
  → useLayoutEffect runs
  → Browser paints
  → useEffect runs
```

**Why this matters:** Side effects that read or write the DOM must go in `useLayoutEffect` or `useEffect`, not in the component body — the render phase may be called multiple times before any commit occurs.

## 🧠 Question 38

**ID**: react-038
**Title**: What is Concurrent React and what does it enable?
**Difficulty**: Hard
**Category**: Concurrent React

### Answer 📄

Concurrent React is a behind-the-scenes change to how React renders component trees, introduced as stable in React 18. It makes React's rendering interruptible, allowing it to work on multiple tasks concurrently and prioritize the most important work.

**The core capability:** React can now start rendering a new tree, pause partway through to handle a higher-priority update (like a keystroke), discard the in-progress work, and restart.

**What it enables:**

1. **`useTransition` / `startTransition`** — mark updates as low-priority so React keeps the UI responsive during heavy renders.

2. **`useDeferredValue`** — defer re-rendering a subtree until the browser is free, similar to debouncing but adaptive.

3. **Automatic batching** — all state updates are batched by default, not just those in event handlers.

4. **Streaming SSR** — React can stream HTML progressively from the server, flushing content as it becomes ready.

5. **Suspense for data fetching** — React can suspend a component, show a fallback, and seamlessly reveal the component when its data is ready.

**Opting in to Concurrent Mode:**

```jsx
// React 18 — concurrent rendering is enabled by default with createRoot
import { createRoot } from 'react-dom/client';
createRoot(document.getElementById('root')).render(<App />);

// Legacy mode — no concurrent features
ReactDOM.render(<App />, document.getElementById('root'));
```

**Important:** concurrent rendering is an opt-in architecture change. Existing apps using `ReactDOM.render` continue to work in legacy mode without concurrent features.

## 🧠 Question 39

**ID**: react-039
**Title**: What is `Suspense` in React and how does it work?
**Difficulty**: Hard
**Category**: Concurrent React

### Answer 📄

`<Suspense>` is a built-in React component that lets you "wait" for something (a lazy-loaded component, async data) and display a fallback UI while waiting.

```jsx
<Suspense fallback={<LoadingSpinner />}>
  <LazyComponent />
</Suspense>
```

**The mechanism — throwing a Promise:**

When a component is not ready to render (its data or code is still loading), it throws a Promise. React's Suspense boundary catches the thrown Promise, shows the `fallback`, and re-renders the component when the Promise resolves.

```jsx
// Simplified internal mechanism
function LazyComponent() {
  const resource = cache.read(); // throws a Promise if loading
  return <div>{resource.data}</div>;
}
```

**Use cases:**

1. **Code splitting** with `React.lazy`:

```jsx
const Chart = lazy(() => import('./Chart'));
<Suspense fallback={<Spinner />}>
  <Chart />
</Suspense>;
```

2. **Data fetching** with frameworks (Next.js, Remix) or libraries (TanStack Query with Suspense mode):

```jsx
// Next.js Server Component — async component suspends automatically
async function UserProfile({ id }) {
  const user = await fetchUser(id);
  return <div>{user.name}</div>;
}
```

**Nested Suspense boundaries** handle loading states independently:

```jsx
<Suspense fallback={<PageSkeleton />}>
  <Header />
  <Suspense fallback={<FeedSkeleton />}>
    <NewsFeed />
  </Suspense>
</Suspense>
```

The inner boundary shows `<FeedSkeleton />` while the feed loads, while the header is already visible.

## 🧠 Question 40

**ID**: react-040
**Title**: What is the `key` prop and what happens when you use index as a key?
**Difficulty**: Medium
**Category**: JSX & Rendering

### Answer 📄

The `key` prop is a special hint React uses during list reconciliation to identify which items changed, were added, or were removed between renders.

**Why index as a key is problematic:**

When you use array index as the key, React maps each index to a component. If the array is reordered, filtered, or items are prepended, the indices shift — React thinks the element at index 0 is the "same" element even though it's now a different item.

This causes:

- **Incorrect state** — a controlled input at index 0 keeps its typed value even though a different item is now at that position.
- **Wrong animations** — transition effects apply to the wrong elements.
- **Stale component state** — `useEffect` cleanup doesn't run between "different" items that happen to share an index.

```jsx
// Bug demonstration
const [items, setItems] = useState(['Alice', 'Bob', 'Carol']);

// After prepending 'Zara':
// Index 0 was 'Alice', now it's 'Zara' — React thinks it just updated props
// React does NOT unmount/remount — old component instance reused
{
  items.map((name, index) => (
    <input key={index} defaultValue={name} /> // will show wrong values
  ));
}

// Fix — use stable IDs
{
  items.map((item) => <input key={item.id} defaultValue={item.name} />);
}
```

**When index as key is acceptable:**

- The list is static and never reordered.
- Items are never added to or removed from the middle of the list.
- No item has stateful children (inputs, animations).
