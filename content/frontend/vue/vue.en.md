---
topic: vue
language: en
version: 2.6
---

# Vue.js Interview Questions

## Available Categories

- Vue Basics
- Reactivity System
- Components
- Composition API
- Directives
- Lifecycle
- State Management
- Routing
- Performance
- Rendering & Internals
- SSR / Hydration
- Advanced Patterns

## Difficulty Levels

- Easy
- Medium
- Hard

## 🧠 Question 1

**ID**: vue-001  
**Title**: What is Vue.js and what problem does it solve?  
**Difficulty**: Easy  
**Category**: Vue Basics

### Answer 📄

Vue.js is a progressive JavaScript framework used for building user interfaces and single-page applications.

It focuses on the **view layer** and allows developers to build interactive interfaces using a component-based architecture.

Vue solves several common frontend problems:

- Managing complex UI state
- Updating the DOM efficiently
- Organizing UI logic into reusable components
- Simplifying reactive data updates

Vue uses a **reactive data-binding system** and a **virtual DOM** to update the interface efficiently when application state changes.

Because it is progressive, Vue can be used gradually, from small interactive widgets to full single-page applications.

## 🧠 Question 2

**ID**: vue-002  
**Title**: What are the core features of Vue.js?  
**Difficulty**: Easy  
**Category**: Vue Basics

### Answer 📄

Vue.js provides several core features that make it suitable for building modern web applications.

Key features include:

- **Reactive data binding**
- **Component-based architecture**
- **Virtual DOM rendering**
- **Computed properties**
- **Watchers**
- **Directives such as v-if, v-for, and v-bind**
- **Vue Router for routing**
- **State management via Pinia or Vuex**

These features help developers build scalable and maintainable front-end applications.

## 🧠 Question 3

**ID**: vue-003  
**Title**: How does Vue differ from React and Angular?  
**Difficulty**: Easy  
**Category**: Vue Basics

### Answer 📄

Vue, React, and Angular are popular tools for building modern web applications, but they differ in design philosophy and complexity.

Vue focuses on simplicity and gradual adoption. It provides an approachable API and built-in solutions for common tasks.

React is primarily a UI library focused on building component-based interfaces. It relies heavily on the surrounding ecosystem for routing and state management.

Angular is a full framework with many built-in features such as dependency injection, form management, and strong TypeScript integration.

In general:

- Vue emphasizes simplicity and developer experience
- React emphasizes flexibility
- Angular emphasizes structure and enterprise-level tooling

## 🧠 Question 4

**ID**: vue-004  
**Title**: What is the Vue instance?  
**Difficulty**: Easy  
**Category**: Vue Basics

### Answer 📄

A Vue instance represents the root of a Vue application.

In Vue 3, applications are created using the `createApp` function. The Vue instance manages the component tree, reactive state, and rendering process.

It acts as the entry point that connects the application logic with the DOM.

A Vue instance typically:

- Holds the root component
- Mounts the application to a DOM element
- Manages lifecycle hooks
- Initializes the reactivity system

Example:

```js
import { createApp } from 'vue';
import App from './App.vue';

const app = createApp(App);

app.use(router);
app.use(pinia);

app.mount('#app');
```

## 🧠 Question 5

**ID**: vue-005  
**Title**: What is the difference between Vue 2 and Vue 3?  
**Difficulty**: Easy  
**Category**: Vue Basics

### Answer 📄

Vue 3 introduced several improvements over Vue 2.

Major differences include:

- The **Composition API** for better logic reuse
- A **new reactivity system based on Proxy**
- **Improved TypeScript support**
- **Better performance and smaller bundle sizes**
- **Fragment support for multiple root elements**
- **Teleport and Suspense components**

Vue 3 provides a more flexible and scalable architecture compared to Vue 2.

## 🧠 Question 6

**ID**: vue-006  
**Title**: What is Vue reactivity and why is it important?  
**Difficulty**: Easy  
**Category**: Reactivity System

### Answer 📄

Vue's reactivity system automatically tracks dependencies between data and the UI.

When reactive data changes, Vue automatically updates the parts of the DOM that depend on that data.

This eliminates the need to manually manipulate the DOM.

Reactivity allows developers to focus on application logic while Vue efficiently handles UI updates.

In Vue 3, this system is implemented using JavaScript Proxy objects.

## 🧠 Question 7

**ID**: vue-007  
**Title**: How does Vue track reactive dependencies?  
**Difficulty**: Medium  
**Category**: Reactivity System

### Answer 📄

Vue tracks reactive dependencies using a dependency tracking system.

When reactive data is accessed during rendering, Vue records that dependency. If the data changes later, Vue knows which components need to be updated.

In Vue 3, this system works using:

- **track()** to record dependencies
- **trigger()** to notify updates

This mechanism ensures that only the necessary parts of the UI are re-rendered.

## 🧠 Question 8

**ID**: vue-008  
**Title**: What are `ref` and `reactive` in Vue 3?  
**Difficulty**: Easy  
**Category**: Reactivity System

### Answer 📄

`ref` and `reactive` are APIs used to create reactive state in Vue 3.

`ref` is used for primitive values or single reactive references.

`reactive` is used for reactive objects.

Both APIs allow Vue to track changes and update the UI automatically.

They are typically used inside the Composition API.

Example:

```js
import { ref, reactive } from 'vue';

const count = ref(0);

const user = reactive({
  name: 'Rasool',
  age: 27,
});

count.value++;
user.age++;
```

## 🧠 Question 9

**ID**: vue-009  
**Title**: What is the difference between `ref` and `reactive`?  
**Difficulty**: Medium  
**Category**: Reactivity System

### Answer 📄

The main difference between `ref` and `reactive` is how they store and access reactive data.

`ref` wraps a value inside an object with a `.value` property.

`reactive` directly converts an object into a reactive proxy.

In general:

- `ref` works best for primitives
- `reactive` works best for objects

Both integrate with Vue's dependency tracking system.

Example:

```js
import { ref, reactive } from 'vue';

// ref — access via .value
const count = ref(0);
count.value++;

// reactive — no .value needed
const user = reactive({ name: 'Rasool', age: 27 });
user.age++;

// Warning: destructuring reactive loses reactivity
const { age } = user; // NOT reactive
```

## 🧠 Question 10

**ID**: vue-010  
**Title**: What are computed properties and how do they differ from methods?  
**Difficulty**: Easy  
**Category**: Reactivity System

### Answer 📄

Computed properties are reactive values that are derived from other reactive data.

They automatically update when their dependencies change.

Unlike methods, computed properties are **cached** based on their dependencies. This means they only re-evaluate when necessary.

Methods execute every time they are called, while computed properties only recompute when their dependencies change.

Example:

```js
import { computed, ref } from 'vue';

const price = ref(100);

const tax = computed(() => {
  return price.value * 0.2;
});
```

## 🧠 Question 11

**ID**: vue-011  
**Title**: What are Vue components and why are they important?  
**Difficulty**: Easy  
**Category**: Components

### Answer 📄

Components are reusable building blocks in Vue applications.

Each component encapsulates its own:

- Template
- Logic
- Styles
- State

This modular architecture allows large applications to be broken into smaller, manageable pieces.

Components improve code reusability, maintainability, and scalability.

Example:

```vue
<!-- UserCard.vue -->
<script setup>
defineProps({ name: String, role: String });
</script>

<template>
  <div class="card">
    <h2>{{ name }}</h2>
    <p>{{ role }}</p>
  </div>
</template>
```

## 🧠 Question 12

**ID**: vue-012  
**Title**: How do props work in Vue?  
**Difficulty**: Easy  
**Category**: Components

### Answer 📄

Props are used to pass data from a parent component to a child component.

They allow components to receive external data while remaining reusable and independent.

Props are declared in the child component and passed via HTML attributes in the parent component.

Vue enforces **one-way data flow**, meaning props flow from parent to child only.

Example:

```vue
<!-- Parent -->
<UserCard name="Rasool" />
```

```vue
<!-- Child -->
<script setup>
defineProps({
  name: String,
});
</script>
```

## 🧠 Question 13

**ID**: vue-013  
**Title**: What is prop validation in Vue?  
**Difficulty**: Medium  
**Category**: Components

### Answer 📄

Prop validation allows developers to specify the expected type and constraints for props.

Vue can check whether the passed value matches the declared type.

Validation options include:

- Type checking
- Required props
- Default values
- Custom validation functions

This improves reliability and prevents incorrect data from being passed into components.

Example:

```js
defineProps({
  title: {
    type: String,
    required: true,
  },
  count: {
    type: Number,
    default: 0,
    validator: (value) => value >= 0,
  },
});
```

## 🧠 Question 14

**ID**: vue-014  
**Title**: What are slots in Vue and why are they useful?  
**Difficulty**: Medium  
**Category**: Components

### Answer 📄

Slots allow parent components to pass template content into child components.

They make components more flexible by allowing dynamic content insertion.

Slots are commonly used for building reusable layout components such as modals, cards, or layout wrappers.

Vue supports default slots, named slots, and scoped slots.

Example:

```vue
<!-- Parent -->
<Card>
  <p>This content is passed from the parent.</p>
</Card>
```

```vue
<!-- Card.vue -->
<template>
  <div class="card">
    <slot></slot>
  </div>
</template>
```

## 🧠 Question 15

**ID**: vue-015  
**Title**: What are scoped slots and how do they differ from regular slots?  
**Difficulty**: Medium  
**Category**: Components

### Answer 📄

Scoped slots allow child components to pass data back to the slot content defined by the parent.

This allows the parent to control rendering while still accessing data from the child component.

They are useful when building reusable components that expose internal state to the slot template.

## 🧠 Question 16

**ID**: vue-016  
**Title**: What is the Composition API in Vue and why was it introduced?  
**Difficulty**: Medium  
**Category**: Composition API

### Answer 📄

The Composition API is a set of APIs introduced in Vue 3 that allows developers to organize component logic by feature rather than by option type.

In the Options API, logic is split across options such as data, methods, computed, and watch. This can make large components difficult to maintain.

The Composition API solves this problem by allowing related logic to be grouped together inside the `setup()` function.

Benefits include:

- Better logic reuse
- Improved code organization
- Easier TypeScript integration
- More scalable architecture for large applications

## 🧠 Question 17

**ID**: vue-017  
**Title**: What is the `setup()` function in Vue?  
**Difficulty**: Medium  
**Category**: Composition API

### Answer 📄

The `setup()` function is the entry point for using the Composition API inside a Vue component.

It runs before the component is created and is responsible for initializing reactive state, computed values, and functions used by the component.

Everything returned from `setup()` becomes available inside the component's template.

The `setup()` function receives two arguments:

- `props`
- `context`

It is commonly used to define component logic in Vue 3 applications.

Example (Q16–Q17):

```js
//Composition API with setup()

import { ref } from 'vue';

export default {
  setup() {
    const count = ref(0);

    const increment = () => {
      count.value++;
    };

    return { count, increment };
  },
};
```

## 🧠 Question 18

**ID**: vue-018  
**Title**: What is a composable in Vue?  
**Difficulty**: Medium  
**Category**: Composition API

### Answer 📄

A composable is a reusable function that encapsulates stateful logic using the Composition API.

Composable functions allow developers to extract logic from components and reuse it across multiple components.

They typically follow the naming convention `useSomething`.

Examples include:

- `useMouse`
- `useFetch`
- `useAuth`

Composable functions improve modularity and code reuse in Vue applications.

Example:

```js
import { ref } from 'vue';

export function useCounter() {
  const count = ref(0);

  const increment = () => {
    count.value++;
  };

  return { count, increment };
}
```

## 🧠 Question 19

**ID**: vue-019  
**Title**: What is the difference between `watch` and `watchEffect`?  
**Difficulty**: Medium  
**Category**: Reactivity System

### Answer 📄

Both `watch` and `watchEffect` are used to react to reactive state changes.

`watch` tracks specific reactive sources and only runs when those sources change.

`watchEffect` automatically tracks all reactive dependencies used inside its callback.

Key differences:

- `watch` requires explicit dependency declaration
- `watchEffect` automatically tracks dependencies
- `watch` provides more control over when updates occur

`watchEffect` is often used for simple reactive side effects.

Example:

```js
//watch vs watchEffect

import { ref, watch, watchEffect } from 'vue';

const count = ref(0);

watch(count, (newValue) => {
  console.log('watch:', newValue);
});

watchEffect(() => {
  console.log('watchEffect:', count.value);
});
```

## 🧠 Question 20

**ID**: vue-020  
**Title**: What are lifecycle hooks in Vue?  
**Difficulty**: Easy  
**Category**: Lifecycle

### Answer 📄

Lifecycle hooks are functions that allow developers to run code at specific stages of a component's lifecycle.

Common lifecycle stages include:

- Component creation
- DOM mounting
- Updates
- Component destruction

Vue provides lifecycle hooks such as:

- `onMounted`
- `onUpdated`
- `onUnmounted`

These hooks allow developers to perform tasks such as data fetching, DOM interaction, or cleanup.

## 🧠 Question 21

**ID**: vue-021  
**Title**: What are the most common lifecycle hooks in Vue 3?  
**Difficulty**: Easy  
**Category**: Lifecycle

### Answer 📄

Vue 3 provides several lifecycle hooks that allow developers to respond to component lifecycle events.

Common hooks include:

- `onBeforeMount`
- `onMounted`
- `onBeforeUpdate`
- `onUpdated`
- `onBeforeUnmount`
- `onUnmounted`

These hooks help manage side effects such as API requests, DOM manipulation, and cleanup operations.

## 🧠 Question 22

**ID**: vue-022  
**Title**: What is `v-if` and how does it differ from `v-show`?  
**Difficulty**: Easy  
**Category**: Directives

### Answer 📄

Both `v-if` and `v-show` are directives used for conditional rendering.

`v-if` conditionally renders elements in the DOM. If the condition is false, the element is not rendered.

`v-show` always renders the element but toggles its visibility using CSS.

In general:

- `v-if` is better for rarely changing conditions
- `v-show` is better for frequently toggled elements

Example:

```vue
<!-- v-if vs v-show -->

<p v-if="isVisible">Visible with v-if</p>

<p v-show="isVisible">Visible with v-show</p>
```

## 🧠 Question 23

**ID**: vue-023  
**Title**: What is `v-for` and how does Vue track list updates?  
**Difficulty**: Medium  
**Category**: Directives

### Answer 📄

`v-for` is a directive used to render lists of items.

Vue requires a `key` attribute when rendering lists so it can efficiently track changes.

The `key` helps Vue identify which items have been added, removed, or reordered.

This allows Vue to update the DOM efficiently using the virtual DOM diffing algorithm.

Example:

```vue
<ul>
  <li v-for="user in users" :key="user.id">
    {{ user.name }}
  </li>
</ul>
```

## 🧠 Question 24

**ID**: vue-024  
**Title**: What is `v-model` and how does it work internally?  
**Difficulty**: Medium  
**Category**: Forms

### Answer 📄

`v-model` is a directive used to create two-way data binding between form inputs and reactive state.

Internally, `v-model` combines:

- `v-bind:value`
- `v-on:input`

When the input changes, Vue updates the bound state. When the state changes, the input value updates automatically.

In Vue 3, `v-model` also supports custom arguments and multiple bindings.

Example:

```vue
<input v-model="username" />
```

```js
const username = ref('');
```

## 🧠 Question 25

**ID**: vue-025  
**Title**: What are custom directives in Vue?  
**Difficulty**: Medium  
**Category**: Directives

### Answer 📄

Custom directives allow developers to create reusable DOM manipulation logic.

They are useful for low-level DOM operations such as:

- Focus management
- Lazy loading images
- Detecting element visibility

Custom directives provide lifecycle hooks similar to components and can be registered globally or locally.

Example:

```js
// Register globally
app.directive('focus', {
  mounted(el) {
    el.focus();
  },
});
```

```vue
<!-- Usage in template -->
<input v-focus />
```

## 🧠 Question 26

**ID**: vue-026  
**Title**: What is `provide` and `inject` in Vue?  
**Difficulty**: Medium  
**Category**: Dependency Injection

### Answer 📄

`provide` and `inject` allow components to share data across the component tree without passing props through every intermediate component.

A parent component can provide values, and any descendant component can inject those values.

This pattern is commonly used for dependency injection and shared services.

Example:

```js
// Parent
import { provide } from 'vue';

provide('theme', 'dark');
```

```js
// Child
import { inject } from 'vue';

const theme = inject('theme');
```

## 🧠 Question 27

**ID**: vue-027  
**Title**: What are dynamic components in Vue?  
**Difficulty**: Medium  
**Category**: Components

### Answer 📄

Dynamic components allow Vue applications to switch between different components at runtime.

This is achieved using the `<component>` element with the `:is` attribute.

Dynamic components are useful for building tab interfaces, dashboards, or conditional component rendering.

Example:

```vue
<component :is="currentComponent"></component>
```

## 🧠 Question 28

**ID**: vue-028  
**Title**: What is the `<KeepAlive>` component in Vue?  
**Difficulty**: Medium  
**Category**: Components

### Answer 📄

`<KeepAlive>` is a built-in component that caches inactive components instead of destroying them.

When a cached component is reactivated, its state is preserved.

This improves performance and user experience when switching between dynamic components.

Example:

```vue
<KeepAlive>
  <component :is="currentComponent" />
</KeepAlive>
```

## 🧠 Question 29

**ID**: vue-029  
**Title**: What is Teleport in Vue?  
**Difficulty**: Medium  
**Category**: Advanced Components

### Answer 📄

Teleport is a Vue feature that allows a component to render part of its template outside of its normal DOM hierarchy.

It is useful for UI elements such as:

- Modals
- Tooltips
- Notifications

Teleport ensures these elements are rendered in the correct place in the DOM while still being managed by Vue.

Example:

```vue
<Teleport to="body">
  <div class="modal">Modal Content</div>
</Teleport>
```

## 🧠 Question 30

**ID**: vue-030  
**Title**: What is Suspense in Vue?  
**Difficulty**: Hard  
**Category**: Advanced Components

### Answer 📄

Suspense is a Vue component used to handle asynchronous components or data dependencies.

It allows developers to define a fallback UI that is displayed while async operations are pending.

Suspense improves user experience by handling loading states in a structured way.

## 🧠 Question 31

**ID**: vue-031  
**Title**: What is `<script setup>` in Vue 3?  
**Difficulty**: Medium  
**Category**: Composition API

### Answer 📄

`<script setup>` is a compile-time syntax introduced in Vue 3 that simplifies the use of the Composition API.

It removes the need to explicitly return values from the `setup()` function.

All variables declared inside `<script setup>` are automatically exposed to the template.

Benefits include:

- Less boilerplate
- Better TypeScript support
- Improved readability
- Faster compilation

Example:

```vue
<script setup>
import { ref } from 'vue';

const count = ref(0);

function increment() {
  count.value++;
}
</script>

<template>
  <button @click="increment">{{ count }}</button>
</template>
```

## 🧠 Question 32

**ID**: vue-032
**Title**: What are `toRef()` and `toRefs()` and when should you use them?
**Difficulty**: Medium
**Category**: Reactivity System

### Answer 📄

`toRef()` creates a ref that is linked to a specific property of a reactive object.

`toRefs()` converts all properties of a reactive object into individual refs.

Both utilities are useful when you need to destructure a reactive object while preserving reactivity.

Without `toRefs()`, destructuring a `reactive` object breaks the reactive connection.

Key differences:

- `toRef()` targets a single property
- `toRefs()` converts all properties at once
- Both keep the link to the original reactive object

Example:

```js
import { reactive, toRef, toRefs } from 'vue';

const state = reactive({ name: 'Rasool', age: 27 });

// toRef — single property stays reactive
const age = toRef(state, 'age');
age.value++; // updates state.age

// toRefs — destructure without losing reactivity
const { name, age: ageRef } = toRefs(state);
name.value = 'Ali'; // updates state.name
```

## 🧠 Question 33

**ID**: vue-033  
**Title**: What is the purpose of `computed()` in Vue?  
**Difficulty**: Easy  
**Category**: Reactivity System

### Answer 📄

`computed()` creates a reactive value that is derived from other reactive state.

Computed properties are cached and only recomputed when their dependencies change.

This improves performance and keeps templates clean.

Computed values are commonly used for derived state such as filtered lists or formatted values.

Example:

```js
import { ref, computed } from 'vue';

const price = ref(100);

const discountedPrice = computed(() => price.value * 0.9);
```

## 🧠 Question 34

**ID**: vue-034
**Title**: What is `defineEmits()` and how do you emit custom events in Vue 3?
**Difficulty**: Medium
**Category**: Components

### Answer 📄

`defineEmits()` is a compiler macro used in `<script setup>` to declare the events a component can emit.

It makes the component's event API explicit and enables type-safe event emission.

Without `defineEmits()`, emitting events still works but loses type-checking and IDE support.

Key benefits:

- Documents which events a component emits
- Enables TypeScript validation of event names and payloads
- Required in `<script setup>` since the `$emit` instance method is not available

Example:

```vue
<script setup>
const emit = defineEmits(['update:count', 'submit']);

function handleClick() {
  emit('update:count', 42);
}
</script>

<template>
  <button @click="handleClick">Click me</button>
</template>
```

## 🧠 Question 35

**ID**: vue-035  
**Title**: What is the Virtual DOM and how does Vue use it?  
**Difficulty**: Medium  
**Category**: Rendering

### Answer 📄

The Virtual DOM is an in-memory representation of the real DOM.

Vue updates the Virtual DOM first when state changes.

It then compares the new Virtual DOM with the previous one using a diffing algorithm.

Finally, Vue applies the minimal set of changes to the real DOM.

This process improves performance by avoiding unnecessary DOM updates.

## 🧠 Question 36

**ID**: vue-036
**Title**: What is Vue Router and how do you set up routing in a Vue application?
**Difficulty**: Medium
**Category**: Routing

### Answer 📄

Vue Router is the official routing library for Vue applications.

It enables navigation between views without full page reloads, which is essential for single-page applications.

Core concepts include:

- **Routes** map URL paths to components
- **`<RouterView>`** renders the matched component for the current URL
- **`<RouterLink>`** creates declarative navigation links

Example:

```js
import { createRouter, createWebHistory } from 'vue-router';
import Home from './views/Home.vue';
import About from './views/About.vue';

const router = createRouter({
  history: createWebHistory(),
  routes: [
    { path: '/', component: Home },
    { path: '/about', component: About },
  ],
});

export default router;
```

```vue
<!-- App.vue -->
<template>
  <nav>
    <RouterLink to="/">Home</RouterLink>
    <RouterLink to="/about">About</RouterLink>
  </nav>
  <RouterView />
</template>
```

## 🧠 Question 37

**ID**: vue-037  
**Title**: What are render functions in Vue?  
**Difficulty**: Hard  
**Category**: Rendering

### Answer 📄

Render functions allow developers to define how a component renders using JavaScript instead of templates.

They provide full programmatic control over the rendering process.

Render functions are rarely used in typical applications but are useful when building:

- UI libraries
- highly dynamic components
- advanced rendering logic

Example:

```js
import { h } from 'vue';

export default {
  render() {
    return h('div', { class: 'container' }, [
      h('h1', 'Hello from render function'),
      h('p', 'This is rendered without a template.'),
    ]);
  },
};
```

## 🧠 Question 38

**ID**: vue-038
**Title**: What are navigation guards in Vue Router?
**Difficulty**: Medium
**Category**: Routing

### Answer 📄

Navigation guards are hooks that allow you to control or cancel route navigation in Vue Router.

They are commonly used for:

- Authentication checks before accessing protected routes
- Redirecting unauthenticated users to a login page
- Preventing navigation when there are unsaved changes

Vue Router provides three types of guards:

- **Global guards** — `router.beforeEach`, `router.afterEach`
- **Per-route guards** — defined in the route config
- **In-component guards** — `onBeforeRouteLeave`, `onBeforeRouteUpdate`

Example:

```js
// Global navigation guard
router.beforeEach((to, from) => {
  const isAuthenticated = !!localStorage.getItem('token');

  if (to.meta.requiresAuth && !isAuthenticated) {
    return { path: '/login' };
  }
});
```

## 🧠 Question 39

**ID**: vue-039
**Title**: How does `v-model` work on custom components in Vue 3?
**Difficulty**: Medium
**Category**: Components

### Answer 📄

In Vue 3, using `v-model` on a custom component expands to a `modelValue` prop and an `update:modelValue` emit.

This allows custom components to support two-way data binding with a clean, readable API.

Vue 3 also supports multiple `v-model` bindings on a single component using named arguments such as `v-model:title` or `v-model:count`.

Example:

```vue
<!-- Parent -->
<CustomInput v-model="username" />
```

```vue
<!-- CustomInput.vue -->
<script setup>
defineProps({ modelValue: String });
const emit = defineEmits(['update:modelValue']);
</script>

<template>
  <input
    :value="modelValue"
    @input="emit('update:modelValue', $event.target.value)"
  />
</template>
```

## 🧠 Question 40

**ID**: vue-040  
**Title**: What is the purpose of the `key` attribute in Vue lists?  
**Difficulty**: Easy  
**Category**: Rendering

### Answer 📄

The `key` attribute helps Vue track elements when rendering lists.

It allows the virtual DOM diffing algorithm to correctly identify which items have changed.

Using unique keys improves performance and prevents unexpected UI behavior.

Example:

```vue
<ul>
  <li v-for="item in items" :key="item.id">
    {{ item.name }}
  </li>
</ul>
```

## 🧠 Question 41

**ID**: vue-041  
**Title**: What are async components in Vue?  
**Difficulty**: Medium  
**Category**: Performance

### Answer 📄

Async components allow components to be loaded lazily.

Instead of loading all components during the initial bundle, Vue loads them only when needed.

This improves application performance and reduces bundle size.

Example:

```js
import { defineAsyncComponent } from 'vue';

const AsyncComponent = defineAsyncComponent(
  () => import('./HeavyComponent.vue'),
);
```

## 🧠 Question 42

**ID**: vue-042  
**Title**: What is code splitting in Vue applications?  
**Difficulty**: Medium  
**Category**: Performance

### Answer 📄

Code splitting is a technique that divides the application bundle into smaller chunks.

These chunks are loaded on demand when users navigate through the application.

Vue applications commonly use dynamic imports to achieve code splitting.

This improves load time and performance.

## 🧠 Question 43

**ID**: vue-043  
**Title**: What is Pinia and why is it used in Vue applications?  
**Difficulty**: Medium  
**Category**: State Management

### Answer 📄

Pinia is the official state management library for Vue.

It replaces Vuex in modern Vue applications.

Pinia provides:

- a simpler API
- better TypeScript support
- modular store architecture
- improved developer experience

### Example (Q43): Pinia Store

```js
import { defineStore } from 'pinia';

export const useCounterStore = defineStore('counter', {
  state: () => ({
    count: 0,
  }),
  actions: {
    increment() {
      this.count++;
    },
  },
});
```

## 🧠 Question 44

**ID**: vue-044  
**Title**: What is server-side rendering (SSR) in Vue?  
**Difficulty**: Hard  
**Category**: Rendering

### Answer 📄

Server-side rendering means rendering Vue components on the server instead of the browser.

The server sends a fully rendered HTML page to the client.

Benefits include:

- improved SEO
- faster initial load time
- better performance for slow devices

## 🧠 Question 45

**ID**: vue-045  
**Title**: What is hydration in Vue SSR?  
**Difficulty**: Hard  
**Category**: Rendering

### Answer 📄

Hydration is the process where Vue attaches event listeners and reactive behavior to server-rendered HTML.

After the browser receives the HTML from the server, Vue reuses that markup instead of recreating it.

This allows the application to become fully interactive while avoiding unnecessary DOM rendering.

## 🧠 Question 46

**ID**: vue-046
**Title**: What is the `<Transition>` component and how does it work in Vue?
**Difficulty**: Medium
**Category**: Advanced Patterns

### Answer 📄

The `<Transition>` component applies CSS transitions or JavaScript animations when an element is inserted into or removed from the DOM.

Vue automatically adds and removes CSS classes at specific stages of the transition lifecycle.

The six transition classes are:

- `v-enter-from`, `v-enter-active`, `v-enter-to` — for entering
- `v-leave-from`, `v-leave-active`, `v-leave-to` — for leaving

`<TransitionGroup>` handles transitions for lists rendered with `v-for`.

Example:

```vue
<Transition name="fade">
  <p v-if="isVisible">Hello</p>
</Transition>
```

```css
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
```

## 🧠 Question 47

**ID**: vue-047
**Title**: How does Vue handle errors and what is `onErrorCaptured`?
**Difficulty**: Hard
**Category**: Advanced Patterns

### Answer 📄

Vue provides several mechanisms for handling errors in components.

`onErrorCaptured` is a lifecycle hook that catches errors thrown by descendant components.

It allows you to implement component-level error boundaries and display fallback UI.

For global error handling, Vue provides `app.config.errorHandler`, which catches any unhandled error in the entire application.

Example:

```js
import { onErrorCaptured, ref } from 'vue';

const hasError = ref(false);
const errorMessage = ref('');

onErrorCaptured((err) => {
  hasError.value = true;
  errorMessage.value = err.message;
  return false; // prevent the error from propagating further
});
```

```js
// Global error handler
app.config.errorHandler = (err, instance, info) => {
  console.error('Global error:', err);
};
```

## 🧠 Question 48

**ID**: vue-048
**Title**: What are `shallowRef()` and `shallowReactive()` in Vue?
**Difficulty**: Hard
**Category**: Reactivity System

### Answer 📄

`shallowRef()` and `shallowReactive()` are performance-focused alternatives to `ref()` and `reactive()`.

`shallowRef()` only makes the top-level `.value` reactive. Nested objects inside are not tracked.

`shallowReactive()` only makes the direct properties of an object reactive. Nested properties are not tracked.

These are useful when working with large data structures or external libraries where deep reactivity would cause unnecessary overhead.

Example:

```js
import { shallowRef, shallowReactive } from 'vue';

const state = shallowRef({ nested: { count: 0 } });

// Triggers reactivity (replaces top-level value)
state.value = { nested: { count: 1 } };

// Does NOT trigger reactivity (mutates nested property)
state.value.nested.count = 2;

// shallowReactive
const form = shallowReactive({ user: { name: 'Rasool' } });
form.user = { name: 'Ali' }; // triggers reactivity
form.user.name = 'Ali'; // does NOT trigger reactivity
```

## 🧠 Question 49

**ID**: vue-049
**Title**: What is `defineExpose()` in Vue 3 and why is it needed?
**Difficulty**: Medium
**Category**: Composition API

### Answer 📄

By default, components using `<script setup>` do not expose any internal state or methods to their parent components.

`defineExpose()` explicitly declares what a child component exposes to parent components through template refs.

This follows the principle of encapsulation — only the intended parts of the component API are accessible from outside.

Example:

```vue
<!-- Child.vue -->
<script setup>
import { ref } from 'vue';

const count = ref(0);

function reset() {
  count.value = 0;
}

defineExpose({ count, reset });
</script>
```

```vue
<!-- Parent.vue -->
<script setup>
import { ref } from 'vue';
import Child from './Child.vue';

const childRef = ref(null);

function resetChild() {
  childRef.value.reset();
}
</script>

<template>
  <Child ref="childRef" />
  <button @click="resetChild">Reset</button>
</template>
```

## 🧠 Question 50

**ID**: vue-050
**Title**: What is programmatic navigation in Vue Router?
**Difficulty**: Medium
**Category**: Routing

### Answer 📄

Programmatic navigation allows you to change routes using JavaScript instead of `<RouterLink>`.

This is useful for redirecting after form submission, login, or any conditional navigation logic.

Vue Router provides two main methods:

- `router.push()` — navigates to a new route and adds an entry to the browser history
- `router.replace()` — navigates to a new route but replaces the current history entry

You can pass a path string or a route location object with a name, params, or query.

Example:

```js
import { useRouter } from 'vue-router';

const router = useRouter();

// Navigate by path
router.push('/dashboard');

// Navigate by named route with params
router.push({ name: 'Profile', params: { id: 42 } });

// Navigate with query string
router.push({ path: '/search', query: { q: 'vue' } });

// Replace current route (no new history entry)
router.replace('/login');
```

## 🧠 Question 51

**ID**: vue-051
**Title**: What is `nextTick()` and why is it needed in Vue?
**Difficulty**: Medium
**Category**: Reactivity System

### Answer 📄

`nextTick()` returns a promise that resolves after Vue has finished flushing all pending DOM updates.

Vue batches DOM updates asynchronously to improve performance. When you change reactive state, the DOM is not updated immediately — it is scheduled for the next microtask tick.

`nextTick()` allows you to wait for the DOM to reflect the latest state before reading it or interacting with it.

Common use cases:

- Reading updated DOM measurements after a state change
- Accessing a newly rendered element via a template ref
- Running assertions in unit tests after triggering reactive state changes

Example:

```js
import { nextTick, ref } from 'vue';

const message = ref('');

async function updateMessage() {
  message.value = 'Updated';

  // DOM is NOT yet updated here
  await nextTick();
  // DOM is now updated
  console.log(document.getElementById('msg').textContent); // 'Updated'
}
```

## 🧠 Question 52

**ID**: vue-052
**Title**: What are the `deep`, `immediate`, and `flush` options in `watch`?
**Difficulty**: Medium
**Category**: Reactivity System

### Answer 📄

The `watch` function accepts an options object that controls how the watcher behaves.

- **`deep: true`** — watches nested properties inside objects or arrays. Without it, only the top-level reference is tracked and nested mutations are ignored.
- **`immediate: true`** — runs the callback immediately when the watcher is created, instead of waiting for the first change.
- **`flush: 'post'`** — defers the callback until after Vue has updated the DOM, allowing access to the updated DOM inside the callback. The default is `'pre'`.

Example:

```js
import { ref, watch } from 'vue';

const user = ref({ name: 'Rasool', age: 27 });

watch(
  user,
  (newValue) => {
    console.log('user changed:', newValue.name);
  },
  {
    deep: true, // detect nested property changes
    immediate: true, // run on component mount
    flush: 'post', // run after DOM updates
  },
);
```

## 🧠 Question 53

**ID**: vue-053
**Title**: What are `markRaw()` and `toRaw()` and when should you use them?
**Difficulty**: Hard
**Category**: Reactivity System

### Answer 📄

`markRaw()` marks an object so it is never converted into a reactive proxy, even if it is placed inside a reactive container.

`toRaw()` returns the original plain JavaScript object from a reactive proxy.

Both are important for performance and compatibility with third-party libraries that break when wrapped in a Vue Proxy.

When to use:

- `markRaw()` — for objects that should never be reactive, such as chart instances, WebGL contexts, or large data structures.
- `toRaw()` — when you need the original object for external APIs, comparisons, or serialization.

Example:

```js
import { reactive, markRaw, toRaw } from 'vue';

class ChartInstance {}

// markRaw — prevent reactivity on a third-party instance
const chart = markRaw(new ChartInstance());
const state = reactive({ chart }); // chart is stored but never proxied

// toRaw — extract the original object from a reactive proxy
const user = reactive({ name: 'Rasool' });
const raw = toRaw(user); // plain JS object
console.log(raw === user); // false — proxy !== original
```

## 🧠 Question 54

**ID**: vue-054
**Title**: What is `readonly()` in Vue and when should you use it?
**Difficulty**: Medium
**Category**: Reactivity System

### Answer 📄

`readonly()` wraps a reactive object and prevents any mutation of it.

Attempting to modify a readonly object logs a warning in development mode and silently fails in production.

It is commonly used to:

- Expose shared state to child components without allowing mutation
- Enforce immutability when using `provide` / `inject`
- Protect store state that should only be modified through defined actions

Example:

```js
import { reactive, readonly, provide } from 'vue';

const state = reactive({ count: 0 });

// Expose a readonly version to descendants
provide('appState', readonly(state));

// Somewhere in a child component:
// appState.count++ // Warning: Set operation on key "count" failed — target is readonly
```

## 🧠 Question 55

**ID**: vue-055
**Title**: What is the Vue plugin system and how do you create a plugin?
**Difficulty**: Medium
**Category**: Advanced Patterns

### Answer 📄

Vue plugins extend the application with reusable, application-level functionality.

A plugin is an object with an `install(app, options)` method, or simply a function with the same signature.

Plugins can:

- Register global components and directives
- Add properties to `app.config.globalProperties`
- Provide application-level values via `app.provide()`
- Install third-party libraries

Example:

```js
// myPlugin.js
export const myPlugin = {
  install(app, options) {
    // Global property accessible as this.$translate in Options API
    app.config.globalProperties.$translate = (key) =>
      options.translations[key] ?? key;

    // Global provide for Composition API
    app.provide('translations', options.translations);

    // Register a global component
    app.component('AppIcon', AppIcon);
  },
};

// main.js
app.use(myPlugin, {
  translations: { welcome: 'Welcome' },
});
```

## 🧠 Question 56

**ID**: vue-056
**Title**: What is `effectScope()` and when is it useful?
**Difficulty**: Hard
**Category**: Reactivity System

### Answer 📄

`effectScope()` creates a scope that captures all reactive effects — computed properties, watchers, and watchEffect calls — created inside it.

All effects within the scope can be stopped simultaneously by calling `scope.stop()`.

This is particularly useful for:

- Vue library authors building composables that create multiple effects
- Dynamically creating and cleaning up groups of reactive effects
- Replacing manual cleanup of multiple independent `watch` calls

Example:

```js
import { effectScope, ref, watch, computed } from 'vue';

const scope = effectScope();

scope.run(() => {
  const count = ref(0);
  const doubled = computed(() => count.value * 2);

  watch(count, (val) => {
    console.log('count:', val);
  });
});

// Dispose all effects inside the scope at once
scope.stop();
```

## 🧠 Question 57

**ID**: vue-057
**Title**: What are `:deep()`, `:slotted()`, and `:global()` in scoped styles?
**Difficulty**: Medium
**Category**: Components

### Answer 📄

When using `<style scoped>`, Vue adds a unique data attribute to all elements so that styles only apply within the current component.

This creates challenges when styling child components or slot content from a parent.

- **`:deep(selector)`** — penetrates the scope boundary to style elements inside child components.
- **`:slotted(selector)`** — targets elements passed into the component via slots.
- **`:global(selector)`** — applies a style globally without any scope attribute, as if placed in a non-scoped style block.

Example:

```vue
<style scoped>
/* Style an element inside a child component */
.wrapper :deep(.child-input) {
  border: 1px solid blue;
}

/* Style content passed via slots */
:slotted(p) {
  font-weight: bold;
}

/* Apply a truly global rule from a scoped block */
:global(.modal-open) {
  overflow: hidden;
}
</style>
```

## 🧠 Question 58

**ID**: vue-058
**Title**: How do you lazy-load routes in Vue Router for code splitting?
**Difficulty**: Medium
**Category**: Routing

### Answer 📄

Lazy-loading routes means each route's component is loaded only when the user navigates to it, instead of including everything in the initial bundle.

This is implemented using dynamic imports: `() => import('./views/Page.vue')`.

Vite and webpack automatically create separate code chunks for each lazy-loaded route, significantly reducing the initial JavaScript payload.

You can also group routes into the same chunk using the webpackChunkName comment or Vite's `rollupOptions`.

Example:

```js
import { createRouter, createWebHistory } from 'vue-router';

const router = createRouter({
  history: createWebHistory(),
  routes: [
    {
      path: '/',
      component: () => import('./views/Home.vue'),
    },
    {
      path: '/admin',
      // loaded only when the user visits /admin
      component: () => import('./views/Admin.vue'),
    },
    {
      path: '/settings',
      // Group into a named chunk
      component: () =>
        import(/* webpackChunkName: "settings" */ './views/Settings.vue'),
    },
  ],
});
```

## 🧠 Question 59

**ID**: vue-059
**Title**: What are functional components in Vue 3 and when should you use them?
**Difficulty**: Hard
**Category**: Performance

### Answer 📄

Functional components are stateless components that render without a component instance.

They are defined as plain JavaScript functions that accept props and a context object containing `slots`, `attrs`, and `emit`.

Because they skip instance creation, they have no lifecycle hooks, no reactive data, and no `this` context.

Functional components are more performant than stateful components for simple rendering logic, but the difference is small in Vue 3 compared to Vue 2.

Use them for purely presentational components that only transform props into a rendered output.

Example:

```js
import { h } from 'vue';

// Functional component as a plain function
const Badge = (props, { slots }) => {
  return h('span', { class: `badge badge-${props.type}` }, slots.default?.());
};

Badge.props = ['type'];
```

## 🧠 Question 60

**ID**: vue-060
**Title**: What are `useAttrs()` and `useSlots()` in the Composition API?
**Difficulty**: Medium
**Category**: Composition API

### Answer 📄

`useAttrs()` returns the non-prop attributes passed to the component — anything not declared as a prop, including `class`, `style`, and event listeners.

`useSlots()` returns the slot functions available to the component.

Both are useful when building transparent wrapper components that need to forward attributes and slots to an inner element.

By default in `<script setup>`, attributes are not automatically applied to the root element unless `inheritAttrs: false` is set. Using `v-bind="attrs"` makes forwarding explicit.

Example:

```vue
<script setup>
import { useAttrs, useSlots } from 'vue';

const attrs = useAttrs();
const slots = useSlots();
</script>

<template>
  <!-- Forward all non-prop attributes to the inner element -->
  <div class="input-wrapper">
    <input v-bind="attrs" />
  </div>
</template>
```

## 🧠 Question 61

**ID**: vue-061
**Title**: How do you clean up side effects inside `watchEffect`?
**Difficulty**: Hard
**Category**: Reactivity System

### Answer 📄

`watchEffect` passes an `onCleanup` function to its callback that lets you cancel or clean up the previous side effect before the effect runs again.

This is critical when performing async operations such as HTTP requests — without cleanup, a previous request could resolve after a newer one, causing a race condition.

`onCleanup` runs before the next execution of the effect and when the component is unmounted.

Example:

```js
import { ref, watchEffect } from 'vue';

const userId = ref(1);

watchEffect((onCleanup) => {
  const controller = new AbortController();

  fetch(`/api/users/${userId.value}`, {
    signal: controller.signal,
  })
    .then((res) => res.json())
    .then((data) => console.log(data))
    .catch((err) => {
      if (err.name !== 'AbortError') console.error(err);
    });

  onCleanup(() => {
    controller.abort(); // cancel in-flight request when userId changes
  });
});
```

## 🧠 Question 62

**ID**: vue-062
**Title**: What are named views in Vue Router?
**Difficulty**: Medium
**Category**: Routing

### Answer 📄

Named views allow multiple `<RouterView>` components to be rendered simultaneously on the same route, each displaying a different component.

This is useful for complex layouts where different parts of the page — such as a sidebar, header, and main content — are each controlled by a separate component.

Each `<RouterView>` is given a `name` attribute, and the route config maps component names to those view names using the `components` (plural) option.

Example:

```js
const router = createRouter({
  routes: [
    {
      path: '/dashboard',
      components: {
        default: DashboardMain,
        sidebar: DashboardSidebar,
        header: DashboardHeader,
      },
    },
  ],
});
```

```vue
<!-- App.vue -->
<template>
  <RouterView name="header" />
  <div class="layout">
    <RouterView name="sidebar" />
    <RouterView />
    <!-- default -->
  </div>
</template>
```

## 🧠 Question 63

**ID**: vue-063
**Title**: How does `app.provide()` differ from component-level `provide`?
**Difficulty**: Medium
**Category**: Advanced Patterns

### Answer 📄

`app.provide()` registers a value at the application level, making it injectable in any component anywhere in the application tree.

Component-level `provide` (inside a component's `setup`) only makes the value available to descendant components in that specific subtree.

`app.provide()` is the recommended way to share global services such as API clients, configuration objects, authentication state, or internationalization helpers.

Example:

```js
// main.js
const app = createApp(App);

app.provide('apiBase', 'https://api.example.com');
app.provide('featureFlags', { darkMode: true, betaFeatures: false });

app.mount('#app');
```

```js
// Any component in the application
import { inject } from 'vue';

const apiBase = inject('apiBase');
const flags = inject('featureFlags');
```

## 🧠 Question 64

**ID**: vue-064
**Title**: How does Vue 3's reactivity system work internally using JavaScript Proxy?
**Difficulty**: Hard
**Category**: Reactivity System

### Answer 📄

Vue 3 replaced Vue 2's `Object.defineProperty`-based reactivity with JavaScript `Proxy`.

When you call `reactive(obj)`, Vue wraps the object in a `Proxy` that intercepts property access and mutation.

During a `get`, Vue calls `track()` to record which reactive effect is currently executing and depends on that property.

During a `set`, Vue calls `trigger()` to notify all recorded effects that depend on the changed property, causing them to re-run.

This approach has key advantages over Vue 2:

- Detects property additions and deletions without special APIs
- Handles arrays natively without wrapping mutation methods
- Supports `Map`, `Set`, `WeakMap`, and `WeakSet`

Example (simplified internals):

```js
function reactive(target) {
  return new Proxy(target, {
    get(target, key, receiver) {
      track(target, key); // record which effect is reading this
      return Reflect.get(target, key, receiver);
    },
    set(target, key, value, receiver) {
      const result = Reflect.set(target, key, value, receiver);
      trigger(target, key); // notify effects that depend on this key
      return result;
    },
  });
}
```

## 🧠 Question 65

**ID**: vue-065
**Title**: What are recursive components in Vue and how do you implement them?
**Difficulty**: Hard
**Category**: Components

### Answer 📄

A recursive component is a component that renders itself within its own template.

This is essential for rendering tree-structured data such as file explorers, nested menus, comment threads, or organizational charts.

In Vue 3 with `<script setup>`, a component can reference itself by its filename automatically. In the Options API, a `name` option is required.

A base case (typically an empty `children` array or null check) must always be included to prevent infinite recursion.

Example:

```vue
<!-- TreeNode.vue -->
<script setup>
defineProps({
  node: {
    type: Object,
    required: true,
  },
});
</script>

<template>
  <li>
    <span>{{ node.label }}</span>
    <ul v-if="node.children?.length">
      <!-- Recursively renders itself for each child -->
      <TreeNode v-for="child in node.children" :key="child.id" :node="child" />
    </ul>
  </li>
</template>
```

## 🧠 Question 66

**ID**: vue-066
**Title**: What is the difference between `created`, `onBeforeMount`, and `mounted` lifecycle hooks?
**Difficulty**: Medium
**Category**: Lifecycle

### Answer 📄

These three hooks fire at different stages of a component's initialization.

**`created`** (Options API) / no direct equivalent in Composition API — the `setup()` function itself runs at this stage. The reactive data is initialized, computed properties and watchers are set up, but the component has not yet been added to the DOM.

**`onBeforeMount`** runs after the render function is compiled and about to execute for the first time, but before the component's DOM nodes are inserted into the document.

**`mounted`** / **`onMounted`** runs after the component's DOM has been created and inserted. This is the correct place to access the real DOM, start subscriptions, measure elements, or initialize third-party libraries that require a DOM node.

```vue
<script setup>
import { onBeforeMount, onMounted } from 'vue';

console.log('setup (= created): DOM not yet available');

onBeforeMount(() => {
  console.log('onBeforeMount: about to render');
});

onMounted(() => {
  console.log('onMounted: DOM is ready');
});
</script>
```

## 🧠 Question 67

**ID**: vue-067
**Title**: What happens internally when a Vue 3 component mounts?
**Difficulty**: Hard
**Category**: Rendering & Internals

### Answer 📄

When a Vue 3 component mounts, the runtime goes through a well-defined sequence:

1. **Component instance is created** — reactive state, computed properties, and watchers are initialized.
2. **`setup()` runs** — the Composition API entry point. Props are resolved, `provide`/`inject` chains are connected.
3. **Render function is compiled** (if using SFC templates, this is done at build time by the Vue compiler).
4. **`onBeforeMount` hooks fire**.
5. **Render effect runs** — the render function executes, producing a virtual DOM tree. During this execution, reactive dependencies are tracked.
6. **Virtual DOM is patched into the real DOM** — Vue's runtime-dom module converts the vnode tree into actual DOM nodes.
7. **`onMounted` hooks fire** — child hooks fire before parent hooks (bottom-up).

After mounting, any reactive dependency change triggers the component's render effect to re-run (producing a new vnode tree), which Vue diffs against the previous tree and patches only the changed DOM nodes.

## 🧠 Question 68

**ID**: vue-068
**Title**: What are the key differences between Vuex and Pinia?
**Difficulty**: Medium
**Category**: State Management

### Answer 📄

Pinia is the official recommended state management library for Vue 3, effectively replacing Vuex.

Key differences:

| Feature         | Vuex                     | Pinia                                    |
| --------------- | ------------------------ | ---------------------------------------- |
| Mutations       | Required to change state | Removed — state is changed directly      |
| Modules         | Nested, verbose setup    | Each store is a flat, independent module |
| TypeScript      | Requires boilerplate     | First-class TypeScript support           |
| Devtools        | Supported                | Supported with better DX                 |
| Bundle size     | Larger                   | Much smaller (~1KB)                      |
| Composition API | Limited support          | Native support with `setup()` stores     |

In Pinia you can use either the Options-style or the setup-style store:

```js
// Pinia - Options store
import { defineStore } from 'pinia';

export const useCounterStore = defineStore('counter', {
  state: () => ({ count: 0 }),
  getters: {
    double: (state) => state.count * 2,
  },
  actions: {
    increment() {
      this.count++;
    },
  },
});

// Pinia - Setup store (Composition API style)
export const useCounterStore = defineStore('counter', () => {
  const count = ref(0);
  const double = computed(() => count.value * 2);
  function increment() {
    count.value++;
  }
  return { count, double, increment };
});
```

## 🧠 Question 69

**ID**: vue-069
**Title**: How do dynamic route parameters work in Vue Router?
**Difficulty**: Medium
**Category**: Routing

### Answer 📄

Dynamic route segments are defined using a colon prefix in the route path. They match any value at that position and expose the matched value via `route.params`.

```js
const routes = [
  { path: '/users/:id', component: UserProfile },
  { path: '/posts/:category/:slug', component: BlogPost },
];
```

Inside a component you access them with `useRoute()`:

```vue
<script setup>
import { useRoute } from 'vue-router';

const route = useRoute();
const userId = route.params.id; // e.g., "42"
</script>
```

**Reacting to param changes** — when navigating between the same route with different params (e.g., `/users/1` → `/users/2`), the component is reused. Use `watch` or `watchEffect` to react:

```js
watch(
  () => route.params.id,
  (newId) => {
    fetchUser(newId);
  },
);
```

**Optional params** use `?` and **multiple matches** use `*` or `+`:

```js
{
  path: '/files/:path*';
} // matches /files/a/b/c
```

## 🧠 Question 70

**ID**: vue-070
**Title**: What is the difference between route params and query params in Vue Router?
**Difficulty**: Easy
**Category**: Routing

### Answer 📄

**Route params** are part of the URL path defined with `:paramName`. They are required by the route pattern and change which route matches.

**Query params** appear after the `?` in the URL and are optional key-value pairs. They do not affect route matching.

```js
// URL: /search?q=vue&page=2
const route = useRoute();
route.params.id; // path param — defined in route definition
route.query.q; // 'vue'
route.query.page; // '2'
```

Programmatic navigation with both:

```js
router.push({
  path: '/users/42',
  query: { tab: 'posts', sort: 'recent' },
});
// → /users/42?tab=posts&sort=recent
```

Use params for resource identity (user ID, article slug) and query params for UI state (filters, pagination, sorting).

## 🧠 Question 71

**ID**: vue-071
**Title**: How does Vue compile `.vue` templates into render functions?
**Difficulty**: Hard
**Category**: Rendering & Internals

### Answer 📄

Vue's template compiler (`@vue/compiler-dom`) transforms `.vue` template strings into JavaScript render functions at build time (via `@vitejs/plugin-vue` or `vue-loader`).

The compilation pipeline has three stages:

1. **Parse** — the template HTML is parsed into an Abstract Syntax Tree (AST).
2. **Transform** — the AST is traversed and optimized. Vue applies transforms for directives (`v-if`, `v-for`), event handlers, slot compilation, and marks static subtrees with `hoistStatic` flags so they are created once outside the render function.
3. **Generate (Code generation)** — the optimized AST is converted into a JavaScript function string.

A simple template like:

```html
<div class="hello">{{ msg }}</div>
```

Compiles to roughly:

```js
import {
  createElementVNode as _createElementVNode,
  toDisplayString as _toDisplayString,
} from 'vue';

function render(_ctx) {
  return _createElementVNode(
    'div',
    { class: 'hello' },
    _toDisplayString(_ctx.msg),
  );
}
```

Static nodes are hoisted above the function so they are only created once, avoiding unnecessary allocations on re-renders. Dynamic nodes are tracked using patch flags (bitwise integers) that tell the runtime exactly what changed.

## 🧠 Question 72

**ID**: vue-072
**Title**: How does the Vue scheduler batch and defer reactive updates?
**Difficulty**: Hard
**Category**: Reactivity System

### Answer 📄

Vue does not update the DOM synchronously when reactive state changes. Instead, it queues the component's re-render and flushes the queue asynchronously in a microtask (using `Promise.then`).

This means multiple synchronous state changes within one task only cause one re-render:

```js
const count = ref(0);

count.value++;
count.value++;
count.value++;
// DOM is updated once, not three times
```

Vue maintains a job queue. When a reactive effect is triggered, Vue calls `queueJob(effect)`. Duplicate jobs (same component render effect) are deduplicated using their internal `id`. After all synchronous code finishes, the microtask runs `flushJobs()`, sorting jobs by their `id` (parent components render before children) and executing them in order.

`nextTick()` returns a promise that resolves after the current flush cycle:

```js
import { nextTick, ref } from 'vue';

const msg = ref('hello');
msg.value = 'world';

await nextTick();
// DOM now reflects 'world'
```

Pre-flush watchers (using `flush: 'pre'`, the default for `watch`) run before the component re-renders. Post-flush watchers (`flush: 'post'`) run after.

## 🧠 Question 73

**ID**: vue-073
**Title**: How does Vue 3's effect tracking work internally (activeEffect and dependency sets)?
**Difficulty**: Hard
**Category**: Reactivity System

### Answer 📄

Vue 3's reactivity is built on two concepts: **effects** (functions that should re-run when dependencies change) and **dependency sets** (sets of effects that read a reactive property).

Internally Vue maintains a global `activeEffect` variable that points to the effect currently executing. During a reactive getter (`get` Proxy trap), Vue's `track()` function:

1. Reads `activeEffect` — if null, nothing is tracked.
2. Looks up (or creates) a `WeakMap<target, Map<key, Set<effect>>>` structure.
3. Adds `activeEffect` to the `Set` for that `target.key` pair.

During a reactive setter (`set` Proxy trap), Vue's `trigger()` function:

1. Looks up the dependency set for `target.key`.
2. Schedules all effects in that set to re-run via the Vue scheduler.

```js
// Simplified pseudocode
let activeEffect = null;
const targetMap = new WeakMap();

function track(target, key) {
  if (!activeEffect) return;
  let depsMap = targetMap.get(target);
  if (!depsMap) targetMap.set(target, (depsMap = new Map()));
  let dep = depsMap.get(key);
  if (!dep) depsMap.set(key, (dep = new Set()));
  dep.add(activeEffect);
}

function trigger(target, key) {
  const depsMap = targetMap.get(target);
  if (!depsMap) return;
  depsMap.get(key)?.forEach((effect) => effect());
}
```

Using a `WeakMap` means the dependency map for an object is garbage-collected when the object itself is.

## 🧠 Question 74

**ID**: vue-074
**Title**: What is the difference between Client-Side Rendering (CSR) and Server-Side Rendering (SSR) in Vue?
**Difficulty**: Medium
**Category**: SSR / Hydration

### Answer 📄

**CSR (Client-Side Rendering)** — the server sends a minimal HTML shell (often just `<div id="app"></div>`) and a JavaScript bundle. The browser downloads the JS, runs Vue, and builds the DOM entirely on the client. Time to First Byte is fast, but the page is blank until JS is parsed and executed (slow Time to Interactive on slow networks).

**SSR (Server-Side Rendering)** — Vue renders the component tree to an HTML string on the server. The browser receives fully-formed HTML immediately (fast First Contentful Paint). After the JS bundle loads, Vue **hydrates** the existing DOM — attaching event listeners and making it interactive without re-rendering.

|             | CSR                  | SSR                     |
| ----------- | -------------------- | ----------------------- |
| First paint | Slow (blank page)    | Fast (HTML ready)       |
| SEO         | Requires extra setup | Excellent               |
| Server load | Low                  | Higher                  |
| Complexity  | Simpler              | Requires Node.js server |

Vue's official SSR solution is **Nuxt.js**, which abstracts the server setup, file-based routing, and hydration strategy (including partial hydration and streaming).

For non-Node SSR, `vue/server-renderer` can output HTML strings from any server environment.

## 🧠 Question 75

**ID**: vue-075
**Title**: What are advanced patterns for `provide` / `inject` — Symbol keys, reactive injection, and defaults?
**Difficulty**: Hard
**Category**: Advanced Patterns

### Answer 📄

`provide` / `inject` is Vue's dependency injection system for sharing data across a component tree without prop drilling.

**Symbol keys** prevent accidental key collisions across libraries or large codebases. Export the Symbol from a shared file:

```js
// keys.js
export const USER_KEY = Symbol('user');
```

```js
// Provider component
import { provide, ref } from 'vue';
import { USER_KEY } from './keys';

const user = ref({ name: 'Alice' });
provide(USER_KEY, user);
```

```js
// Descendant component
import { inject } from 'vue';
import { USER_KEY } from './keys';

const user = inject(USER_KEY); // fully typed if using TypeScript
```

**Reactive injection** — providing a `ref` or `reactive` value keeps the injected value live. The consumer sees changes automatically:

```js
// In provider
const theme = ref('light');
provide('theme', theme); // provide the ref itself, not theme.value

// In consumer
const theme = inject('theme'); // theme is a Ref<string>
```

**Default values** — the second argument to `inject` is a fallback used when no provider is found:

```js
const theme = inject('theme', ref('light'));
// Or a factory function for expensive defaults:
const config = inject('config', () => ({ debug: false }), true);
```

**Read-only injection** — wrap with `readonly()` before providing to prevent consumers from mutating the value.

## 🧠 Question 76

**ID**: vue-076
**Title**: What is the Vue rendering pipeline from state change to DOM update?
**Difficulty**: Hard
**Category**: Rendering & Internals

### Answer 📄

When reactive state changes, Vue's rendering pipeline follows these steps:

1. **Trigger** — a reactive setter calls `trigger()`, scheduling the component's render effect in the job queue.
2. **Scheduler flush** — on the next microtask, `flushJobs()` runs, processing queued render effects in parent-first order.
3. **Re-render** — the component's render function runs, accessing reactive state (which is tracked) and producing a new **virtual DOM (vnode) tree**.
4. **Diff (patch)** — Vue compares the new vnode tree to the previous tree. Using **patch flags** set by the compiler, Vue knows exactly which nodes and attributes are dynamic, skipping static parts entirely.
5. **DOM update** — only the nodes that changed are updated in the real DOM via the runtime-dom module.
6. **Post-flush hooks** — `onUpdated` hooks fire, and `watchEffect` / `watch` post-flush callbacks run.

The compiler's static hoisting and patch flags are critical for performance — they allow the runtime to skip large subtrees that didn't change, making Vue updates sub-linear relative to tree size.

## 🧠 Question 77

**ID**: vue-077
**Title**: What are the different component communication patterns in Vue?
**Difficulty**: Medium
**Category**: Components

### Answer 📄

Vue provides several mechanisms for components to communicate:

**1. Props (parent → child)** — the standard way to pass data down:

```js
defineProps({ title: String, count: Number });
```

**2. Emits (child → parent)** — the child fires events the parent listens to:

```js
const emit = defineEmits(['update:modelValue', 'close']);
emit('close');
```

**3. v-model** — two-way binding shorthand using props + emits:

```html
<MyInput v-model="text" />
<!-- expands to: :modelValue="text" @update:modelValue="text = $event" -->
```

**4. provide / inject** — ancestor → any descendant, bypasses intermediate components.

**5. Pinia / Vuex** — cross-component state in a centralized store.

**6. Template refs + defineExpose** — parent directly calls methods or reads state from a child:

```js
// Child exposes
defineExpose({ reset, validate });
// Parent
const formRef = ref(null);
formRef.value.validate();
```

**7. Event bus** — using a tiny mitt instance for truly decoupled communication between unrelated components. Use sparingly.

## 🧠 Question 78

**ID**: vue-078
**Title**: What is `<Teleport>` and when should you use it?
**Difficulty**: Medium
**Category**: Advanced Patterns

### Answer 📄

`<Teleport>` renders its slot content into a different DOM node than where the component logically lives in the component tree.

This is essential for modals, tooltips, dropdowns, and notifications — UI that must escape CSS `overflow: hidden` or `z-index` stacking contexts imposed by parent elements.

```vue
<template>
  <button @click="open = true">Open Modal</button>

  <Teleport to="body">
    <div v-if="open" class="modal-overlay">
      <div class="modal">
        <p>Modal content</p>
        <button @click="open = false">Close</button>
      </div>
    </div>
  </Teleport>
</template>
```

The `to` attribute accepts a CSS selector or an actual DOM element. The teleported content remains part of the component's logical tree — it inherits `provide`/`inject` from its parent component, and its event handlers work normally.

`disabled` prop lets you conditionally disable teleporting:

```vue
<Teleport to="body" :disabled="isMobile">...</Teleport>
```

Multiple teleports can target the same container and are appended in order.

## 🧠 Question 79

**ID**: vue-079
**Title**: What is `<Suspense>` and how does it handle async components?
**Difficulty**: Hard
**Category**: Advanced Patterns

### Answer 📄

`<Suspense>` is a built-in Vue component that coordinates the loading state of multiple async operations in its component subtree, showing fallback content until all async dependencies resolve.

It has two named slots:

- `#default` — the actual content (may contain async components or components with async `setup()`)
- `#fallback` — shown while any default-slot component is still loading

```vue
<Suspense>
  <template #default>
    <AsyncDashboard />  <!-- has async setup() -->
  </template>
  <template #fallback>
    <LoadingSpinner />
  </template>
</Suspense>
```

An async `setup()` is a component whose `setup` function is `async` or returns a Promise:

```vue
<script setup>
const data = await fetch('/api/dashboard').then((r) => r.json());
</script>
```

`<Suspense>` emits `@pending`, `@resolve`, and `@fallback` events for fine-grained control.

**Nesting**: child `<Suspense>` boundaries handle their own loading independently.

**Note**: `<Suspense>` is still experimental in some configurations and works best when combined with SSR streaming in frameworks like Nuxt 3.

## 🧠 Question 80

**ID**: vue-080
**Title**: What are `v-model` modifiers and how do you create custom ones?
**Difficulty**: Medium
**Category**: Directives

### Answer 📄

Vue provides built-in `v-model` modifiers that transform the bound value:

- `.trim` — strips leading/trailing whitespace from strings
- `.number` — converts the input value to a number using `parseFloat`
- `.lazy` — syncs the value on `change` event instead of `input`

```html
<input v-model.trim.lazy="username" />
```

**Custom modifiers** — when using `v-model` on a custom component, modifiers are passed as a `modelModifiers` prop (or `[propName]Modifiers` for named v-models):

```vue
<!-- Parent -->
<MyInput v-model.capitalize="text" />
```

```vue
<!-- MyInput.vue -->
<script setup>
const props = defineProps({
  modelValue: String,
  modelModifiers: { default: () => ({}) },
});
const emit = defineEmits(['update:modelValue']);

function handleInput(e) {
  let value = e.target.value;
  if (props.modelModifiers.capitalize) {
    value = value.charAt(0).toUpperCase() + value.slice(1);
  }
  emit('update:modelValue', value);
}
</script>

<template>
  <input :value="modelValue" @input="handleInput" />
</template>
```
