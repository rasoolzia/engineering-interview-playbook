---
topic: javascript
language: en
version: 1.2
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

## 🧠 Question 11

**ID**: js-011  
**Title**: What is an execution context in JavaScript?  
**Difficulty**: Medium  
**Category**: Execution Context & Scope

### Answer 📄

An execution context is the environment in which JavaScript code is evaluated and executed.

There are three types of execution contexts:

- Global Execution Context
- Function Execution Context
- Eval Execution Context

Each execution context consists of two phases:

1. Creation Phase
2. Execution Phase

During the creation phase, variables and function declarations are stored in memory. During the execution phase, code runs line by line.

Execution contexts are managed using the call stack.

```javascript
// Execution Context

function greet(name) {
  return 'Hello ' + name;
}

greet('Rasool');
```

## 🧠 Question 12

**ID**: js-012  
**Title**: What happens during the creation phase of an execution context?  
**Difficulty**: Medium  
**Category**: Execution Context & Scope

### Answer 📄

During the creation phase:

- The scope chain is determined.
- The variable environment is created.
- The `this` binding is established.
- Function declarations are fully initialized.
- Variables declared with `var` are initialized with undefined.
- Variables declared with `let` and `const` are placed in the Temporal Dead Zone.

No code is executed during this phase.

```javascript
// Creation Phase

console.log(x); // undefined
var x = 5;

function test() {}
```

## 🧠 Question 13

**ID**: js-013  
**Title**: What is the call stack and how does it work?  
**Difficulty**: Medium  
**Category**: Engine & Runtime

### Answer 📄

The call stack is a data structure that keeps track of function execution.

When a function is invoked, a new execution context is pushed onto the stack.

When a function completes, its execution context is removed from the stack.

If the stack exceeds its maximum size due to excessive recursion, a stack overflow error occurs.

```javascript
// Call Stack

function first() {
  second();
}

function second() {
  third();
}

function third() {
  console.log('Inside third');
}

first();
```

## 🧠 Question 14

**ID**: js-014  
**Title**: What is the Temporal Dead Zone (TDZ)?  
**Difficulty**: Medium  
**Category**: Execution Context & Scope

### Answer 📄

The Temporal Dead Zone is the time between entering a block and the actual declaration of a variable using `let` or `const`.

During this period, accessing the variable results in a ReferenceError.

Although `let` and `const` declarations are hoisted, they are not initialized until execution reaches their declaration line.

```javascript
// Temporal Dead Zone

{
  // console.log(a); // ReferenceError
  let a = 10;
}
```

## 🧠 Question 15

**ID**: js-015  
**Title**: How does the `this` keyword work in JavaScript?  
**Difficulty**: Medium  
**Category**: Functions

### Answer 📄

The value of `this` depends on how a function is called.

- In the global context, `this` refers to the global object.
- In a regular function call, `this` depends on strict mode.
- In a method call, `this` refers to the object that owns the method.
- In arrow functions, `this` is lexically inherited from the surrounding scope.
- In constructor functions, `this` refers to the newly created instance.

```javascript
// this behavior

const obj = {
  name: 'Ali',
  greet() {
    console.log(this.name);
  },
};

obj.greet(); // Ali
```

## 🧠 Question 16

**ID**: js-016  
**Title**: What is the difference between regular functions and arrow functions?  
**Difficulty**: Medium  
**Category**: Functions

### Answer 📄

Arrow functions differ from regular functions in several ways:

- They do not have their own `this`.
- They do not have their own `arguments` object.
- They cannot be used as constructors.
- They are always anonymous.

Arrow functions inherit `this` from their lexical scope.

```javascript
// Arrow vs Regular

const obj = {
  name: 'Sara',
  regular() {
    console.log(this.name);
  },
  arrow: () => {
    console.log(this.name);
  },
};

obj.regular(); // Sara
obj.arrow(); // undefined
```

## 🧠 Question 17

**ID**: js-017  
**Title**: What is the difference between shallow copy and deep copy?  
**Difficulty**: Medium  
**Category**: Memory & References

### Answer 📄

A shallow copy creates a new object but copies references for nested objects.

A deep copy creates a completely independent clone, including all nested objects.

Modifying nested properties in a shallow copy affects the original object, while a deep copy prevents this behavior.

```javascript
// Shallow Copy

const original = { info: { age: 20 } };
const copy = { ...original };

copy.info.age = 30;

console.log(original.info.age); // 30
```

## 🧠 Question 18

**ID**: js-018  
**Title**: What are microtasks and macrotasks in the event loop?  
**Difficulty**: Hard  
**Category**: Asynchronous & Event Loop

### Answer 📄

In JavaScript’s event loop:

- Macrotasks include tasks such as timers and I/O operations.
- Microtasks include Promise callbacks and mutation observers.

After each macrotask completes, all microtasks in the queue are executed before the next macrotask begins.

Microtasks have higher priority than macrotasks.

```javascript
// Microtask vs Macrotask

console.log('Start');

setTimeout(() => console.log('Macrotask'), 0);

Promise.resolve().then(() => {
  console.log('Microtask');
});

console.log('End');

// Output:
// Start
// End
// Microtask
// Macrotask
```

## 🧠 Question 19

**ID**: js-019  
**Title**: What are the different states of a Promise?  
**Difficulty**: Medium  
**Category**: Asynchronous & Event Loop

### Answer 📄

A Promise has three states:

- Pending
- Fulfilled
- Rejected

Once a Promise is fulfilled or rejected, its state becomes settled and cannot change.

Promise handlers are executed asynchronously.

```javascript
// Promise states

const promise = new Promise((resolve, reject) => {
  resolve('Done');
});

promise.then((result) => console.log(result));
```

## 🧠 Question 20

**ID**: js-020  
**Title**: How does async/await work internally?  
**Difficulty**: Hard  
**Category**: Asynchronous & Event Loop

### Answer 📄

Async/await is syntactic sugar built on top of Promises.

An async function always returns a Promise.

The await keyword pauses execution of the async function until the Promise resolves, but it does not block the main thread.

Internally, async/await transforms asynchronous code into a structure similar to chained Promise calls.

```javascript
// async/await

async function fetchData() {
  return 'Data loaded';
}

fetchData().then(console.log);
```
