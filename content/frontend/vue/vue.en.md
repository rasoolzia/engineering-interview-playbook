---
topic: vue
language: en
version: 1.3
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
import { ref, reactive } from 'vue';

const count = ref(0);

const user = reactive({
  name: 'Rasool',
  age: 27,
});

count.value++;
user.age++;
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
