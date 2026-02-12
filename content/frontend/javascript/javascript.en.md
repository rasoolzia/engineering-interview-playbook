---
topic: javascript
language: en
version: 1.1
---

# JavaScript Interview Questions

## Available Categories

- Fundamentals
- Execution Context & Scope
- Memory & References
- Functions
- Asynchronous & Event Loop
- Engine & Runtime

## Difficulty Levels

- Easy
- Medium
- Hard

## 🧠 Question 1

**ID**: js-001  
**Title**: What is JavaScript and how does it differ from compiled languages?  
**Difficulty**: Easy  
**Category**: Fundamentals

### Answer 📄

JavaScript is a high-level, interpreted programming language primarily used for building interactive web applications. It runs inside the browser as well as on servers using environments like Node.js.

Unlike compiled languages such as C or C++, JavaScript does not require a separate compilation step before execution. Instead, it is executed by a JavaScript engine at runtime.

Modern JavaScript engines internally use Just-In-Time (JIT) compilation to optimize performance, which makes JavaScript fast while still behaving like an interpreted language from the developer’s perspective.

## 🧠 Question 2

**ID**: js-002  
**Title**: What are the primitive data types in JavaScript?  
**Difficulty**: Easy  
**Category**: Fundamentals

### Answer 📄

JavaScript has seven primitive data types:

- String
- Number
- BigInt
- Boolean
- Undefined
- Null
- Symbol

Primitive values are immutable and are stored directly in memory. When assigned to a new variable, a copy of the value is created.

## 🧠 Question 3

**ID**: js-003  
**Title**: What is the difference between null and undefined?  
**Difficulty**: Easy  
**Category**: Fundamentals

### Answer 📄

`undefined` means a variable has been declared but has not been assigned a value.

`null` is an intentional assignment that represents the absence of any object value.

In short:

- `undefined` is the default state of uninitialized variables.
- `null` is explicitly assigned by the developer to indicate “no value”.

## 🧠 Question 4

**ID**: js-004  
**Title**: What is the difference between var, let, and const?  
**Difficulty**: Easy  
**Category**: Fundamentals

### Answer 📄

`var`, `let`, and `const` are used to declare variables, but they differ in scope and behavior.

- `var` is function-scoped and allows redeclaration.
- `let` is block-scoped and does not allow redeclaration in the same scope.
- `const` is block-scoped and cannot be reassigned after initialization.

Additionally, variables declared with `let` and `const` are not accessible before initialization due to the Temporal Dead Zone.

```javascript
// var vs let
{
  var x = 10;
  let y = 20;
}

console.log(x); // 10
console.log(y); // ReferenceError
```

## 🧠 Question 5

**ID**: js-005  
**Title**: What is scope in JavaScript?  
**Difficulty**: Medium  
**Category**: Execution Context & Scope

### Answer 📄

Scope determines the accessibility of variables and functions in different parts of the code.

JavaScript has three main types of scope:

- Global Scope: Accessible everywhere in the program.
- Function Scope: Accessible only within a specific function.
- Block Scope: Accessible only inside a block defined by curly braces.

Scope is determined lexically, meaning it depends on where variables are written in the code, not where they are executed.

## 🧠 Question 6

**ID**: js-006  
**Title**: What is hoisting in JavaScript?  
**Difficulty**: Medium  
**Category**: Execution Context & Scope

### Answer 📄

Hoisting is JavaScript’s default behavior of moving variable and function declarations to the top of their containing scope during the creation phase of execution.

Function declarations are fully hoisted.

Variables declared with `var` are hoisted but initialized with `undefined`.

Variables declared with `let` and `const` are hoisted but remain in the Temporal Dead Zone until initialized.

```javascript
// Hoisting behavior

console.log(a); // undefined
var a = 5;

console.log(b); // ReferenceError
let b = 10;
```

## 🧠 Question 7

**ID**: js-007  
**Title**: What is the difference between primitive values and reference values?  
**Difficulty**: Medium  
**Category**: Memory & References

### Answer 📄

Primitive values are stored directly in memory and are immutable.

Reference values such as objects and arrays are stored in the heap, and variables hold references to their memory location.

When a primitive is assigned to another variable, a copy is created.

When a reference value is assigned, both variables point to the same memory location.

```javascript
// Primitive vs Reference

let a = 10;
let b = a;
b = 20;

console.log(a); // 10

let obj1 = { name: 'Ali' };
let obj2 = obj1;
obj2.name = 'Sara';

console.log(obj1.name); // Sara
```

## 🧠 Question 8

**ID**: js-008  
**Title**: How does memory management work in JavaScript?  
**Difficulty**: Medium  
**Category**: Memory & References

### Answer 📄

JavaScript automatically allocates memory when variables are declared and frees it when it is no longer needed.

Memory management relies on garbage collection.

Most modern JavaScript engines use a mark-and-sweep algorithm to identify unused objects. If an object is no longer reachable from the root (such as the global object), it becomes eligible for garbage collection.

## 🧠 Question 9

**ID**: js-009  
**Title**: What is a closure in JavaScript?  
**Difficulty**: Medium  
**Category**: Functions

### Answer 📄

A closure is a function that remembers variables from its lexical scope even after the outer function has finished executing.

Closures allow functions to access variables that were available at the time they were created.

They are commonly used for data privacy, function factories, and maintaining state in asynchronous code.

```javascript
// Closure

function outer() {
  let count = 0;

  return function inner() {
    count++;
    return count;
  };
}

const counter = outer();
console.log(counter()); // 1
console.log(counter()); // 2
```

## 🧠 Question 10

**ID**: js-010  
**Title**: What is the event loop in JavaScript?  
**Difficulty**: Medium  
**Category**: Asynchronous & Event Loop

### Answer 📄

JavaScript is single-threaded, meaning it has one call stack.

The event loop is a mechanism that allows JavaScript to handle asynchronous operations without blocking execution.

It continuously checks whether the call stack is empty. If it is, it takes tasks from the callback queue and pushes them onto the stack for execution.

This mechanism enables non-blocking behavior while maintaining a single-threaded model.

```javascript
// Event Loop

console.log('Start');

setTimeout(() => {
  console.log('Timeout');
}, 0);

console.log('End');

// Output:
// Start
// End
// Timeout
```
