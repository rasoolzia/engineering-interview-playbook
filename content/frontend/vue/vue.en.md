---
topic: vue
language: en
version: 2.0
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

```js
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

```js
<!-- Parent -->
<UserCard name="Rasool" />
```

```js
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

```js
<!-- Parent -->
<Card>
  <p>This content is passed from the parent.</p>
</Card>
```

```js
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

```js
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

```js
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

```js
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

```js
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

```js
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

```js
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

```js
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

```js
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

```js
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

```js
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

```js
<!-- Parent -->
<CustomInput v-model="username" />
```

```js
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

```js
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
