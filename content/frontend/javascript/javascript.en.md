---
topic: javascript
language: en
version: 1.7
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

Example:

```js
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

Example:

```js
let globalVar = 'global'; // Global Scope

function example() {
  let funcVar = 'function'; // Function Scope

  if (true) {
    let blockVar = 'block'; // Block Scope
    console.log(blockVar); // block
  }

  // console.log(blockVar); // ReferenceError
}
```

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

Example:

```js
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

Example:

```js
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

Example:

```js
let user = { name: 'Rasool' }; // memory allocated

user = null; // reference removed → eligible for garbage collection
```

## 🧠 Question 9

**ID**: js-009  
**Title**: What is a closure in JavaScript?  
**Difficulty**: Medium  
**Category**: Functions

### Answer 📄

A closure is a function that remembers variables from its lexical scope even after the outer function has finished executing.

Closures allow functions to access variables that were available at the time they were created.

They are commonly used for data privacy, function factories, and maintaining state in asynchronous code.

Example:

```js
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

Example:

```js
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

Example:

```js
// Global Execution Context is created first
const name = 'Rasool';

function greet() {
  // Function Execution Context is created when greet() is called
  const message = 'Hello ' + name; // accesses global scope via scope chain
  return message;
}

console.log(greet()); // Hello Rasool
// After greet() returns, its execution context is removed from the stack
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

Example:

```js
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

Example:

```js
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

Example:

```js
// Temporal Dead Zone

{
  console.log(a); // ReferenceError: Cannot access 'a' before initialization
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

Example:

```js
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

Example:

```js
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

Example:

```js
// Shallow Copy — nested objects are still shared

const original = { info: { age: 20 } };
const shallow = { ...original };

shallow.info.age = 30;

console.log(original.info.age); // 30 (original was mutated)
```

```js
// Deep Copy — completely independent clone

const original = { info: { age: 20 } };
const deep = JSON.parse(JSON.stringify(original));

deep.info.age = 30;

console.log(original.info.age); // 20 (original is unchanged)
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

Example:

```js
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

Example:

```js
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

Example:

```js
// async/await — await pauses the function, not the main thread

function delay(ms) {
  return new Promise((resolve) => setTimeout(resolve, ms));
}

async function run() {
  console.log('Before await');
  await delay(1000);
  console.log('After await'); // runs after 1 second
}

run();
console.log('This runs immediately');

// Output:
// Before await
// This runs immediately
// After await
```

## 🧠 Question 21

**ID**: js-021  
**Title**: What is a prototype in JavaScript?  
**Difficulty**: Medium  
**Category**: Objects & Prototypes

### Answer 📄

A prototype is an object from which other objects inherit properties and methods.

Every JavaScript object has an internal link to another object called its prototype. When a property is accessed on an object, JavaScript first looks for it on the object itself. If not found, it looks up the prototype chain.

This mechanism is known as prototypal inheritance.

Example:

```js
function Person(name) {
  this.name = name;
}

Person.prototype.sayHello = function () {
  return `Hi, I'm ${this.name}`;
};

const user = new Person('Rasool');

console.log(user.sayHello()); // Hi, I'm Rasool
console.log(user.__proto__ === Person.prototype); // true
```

## 🧠 Question 22

**ID**: js-022  
**Title**: What is the prototype chain and how does property lookup work?  
**Difficulty**: Hard  
**Category**: Objects & Prototypes

### Answer 📄

The prototype chain is a series of linked objects that JavaScript uses to resolve property access.

When a property is requested:

1. The engine checks the object itself.
2. If not found, it checks the object's prototype.
3. This continues until reaching null.

If the property is not found anywhere in the chain, undefined is returned.

This lookup process enables inheritance in JavaScript.

Example:

```js
const animal = {
  eats: true,
};

const dog = Object.create(animal);
dog.barks = true;

console.log(dog.barks); // true (own property)
console.log(dog.eats); // true (inherited from prototype)
console.log(dog.hasOwnProperty('eats')); // false
```

## 🧠 Question 23

**ID**: js-023  
**Title**: What is the difference between `__proto__` and `prototype`?  
**Difficulty**: Hard  
**Category**: Objects & Prototypes

### Answer 📄

`prototype` is a property of constructor functions. It defines what will become the prototype of instances created with that constructor.

`__proto__` is an accessor property available on objects that points to their internal prototype.

In simple terms:

- `prototype` exists on functions.
- `__proto__` exists on objects.

Example:

```js
function Car() {}

const myCar = new Car();

console.log(Car.prototype === myCar.__proto__); // true
console.log(typeof Car.prototype); // object
console.log(typeof myCar.prototype); // undefined
```

`prototype` is on the function  
`__proto__` on the object created

## 🧠 Question 24

**ID**: js-024  
**Title**: How does inheritance work in JavaScript?  
**Difficulty**: Medium  
**Category**: Objects & Prototypes

### Answer 📄

Inheritance in JavaScript is based on prototypes.

Objects inherit properties and methods from other objects via the prototype chain.

This can be achieved using constructor functions, Object.create, or ES6 classes.

Unlike classical inheritance in other languages, JavaScript uses prototypal inheritance.

Example:

```js
class Animal {
  speak() {
    return 'Some sound';
  }
}

class Cat extends Animal {
  speak() {
    return 'Meow';
  }
}

const kitty = new Cat();

console.log(kitty.speak()); // Meow
```

Behind the scenes, it works the same with prototype, only the syntax is cleaner.

## 🧠 Question 25

**ID**: js-025  
**Title**: What is strict mode in JavaScript and why is it important?  
**Difficulty**: Medium  
**Category**: Language Behavior

### Answer 📄

Strict mode is a way to opt into a restricted version of JavaScript.

It eliminates some silent errors by throwing exceptions and prevents unsafe actions such as:

- Creating global variables accidentally
- Assigning to non-writable properties
- Using duplicate parameter names

Strict mode makes code more secure and easier to optimize.

Example:

```js
'use strict';

x = 10; // ReferenceError: x is not defined

function test(a, a) {
  // SyntaxError: Duplicate parameter name not allowed in this context
  return a;
}
```

Without strict mode, these errors would be silently ignored.
With strict mode, the engine throws immediately, making bugs easier to detect.

## 🧠 Question 26

**ID**: js-026  
**Title**: What are JavaScript modules and how do they work?  
**Difficulty**: Medium  
**Category**: Modules & Architecture

### Answer 📄

JavaScript modules allow code to be split into reusable, isolated files.

Modules use export to expose functionality and import to consume it.

Each module has its own scope and executes only once.

ES Modules are the standard module system in modern JavaScript.

Example:

```js
// math.js

export function add(a, b) {
  return a + b;
}
```

```js
// app.js

import { add } from './math.js';

console.log(add(2, 3)); // 5
```

Each file has a separate scope.  
The load is only done once.

## 🧠 Question 27

**ID**: js-027  
**Title**: What is a memory leak and how can it happen in JavaScript?  
**Difficulty**: Hard  
**Category**: Memory & Performance

### Answer 📄

A memory leak occurs when memory that is no longer needed is not released.

In JavaScript, memory leaks often happen due to:

- Unused references being retained
- Closures holding large objects
- Forgotten timers or event listeners
- Detached DOM elements still referenced in code

Memory leaks degrade performance over time.

Example:

```js
function startTimer() {
  const largeData = new Array(1000000).fill('leak');

  setInterval(() => {
    console.log(largeData.length);
  }, 1000);
}

startTimer();
```

Here `largeData` gets stuck in the closure.  
It won't be garbage collected until the interval is cleared.

Solution:

```js
const interval = setInterval(() => {
  console.log('running');
}, 1000);

clearInterval(interval);
```

## 🧠 Question 28

**ID**: js-028  
**Title**: What are WeakMap and WeakSet and how are they different from Map and Set?  
**Difficulty**: Hard  
**Category**: Memory & Performance

### Answer 📄

WeakMap and WeakSet are similar to Map and Set but hold weak references to objects.

If no other references to the key or value exist, the garbage collector can reclaim that memory automatically.

Key differences:

- **WeakMap**: stores key-value pairs where keys must be objects. Keys are weakly referenced.
- **WeakSet**: stores a collection of objects. Values are weakly referenced.
- Neither WeakMap nor WeakSet is iterable.

Example:

```js
// WeakMap — key is weakly held
let obj = { name: 'Rasool' };

const map = new Map();
map.set(obj, 'data');

const weakMap = new WeakMap();
weakMap.set(obj, 'data');

obj = null;
// map still holds the reference → no garbage collection
// weakMap releases the reference → eligible for garbage collection
```

```js
// WeakSet — object is weakly held
let user = { id: 1 };

const weakSet = new WeakSet();
weakSet.add(user);

console.log(weakSet.has(user)); // true

user = null;
// user is now eligible for garbage collection
// weakSet no longer holds it
```

> **_NOTE:_** WeakMap and WeakSet are not iterable and have no `size` property.

## 🧠 Question 29

**ID**: js-029  
**Title**: How does JavaScript handle object property descriptors?  
**Difficulty**: Hard  
**Category**: Objects & Internals

### Answer 📄

Each property in a JavaScript object has descriptors that define its behavior.

Property descriptors include:

- value
- writable
- enumerable
- configurable
- get
- set

These descriptors control whether a property can be modified, deleted, or enumerated.

Example:

```js
const user = {};

Object.defineProperty(user, 'name', {
  value: 'Rasool',
  writable: false,
  enumerable: true,
  configurable: false,
});

user.name = 'Ali'; // Does not change

console.log(user.name); // Rasool
```

The descriptor determines how the property behaves.

## 🧠 Question 30

**ID**: js-030  
**Title**: How do JavaScript engines optimize code execution?  
**Difficulty**: Hard  
**Category**: Engine & Runtime

### Answer 📄

Modern JavaScript engines use techniques such as Just-In-Time compilation to improve performance.

They analyze code at runtime, optimize frequently executed paths, and apply inline caching.

However, certain patterns such as changing object shapes dynamically can cause de-optimization.

Understanding engine behavior helps write more performant code.

Example:

```js
function createUser(name) {
  return { name };
}

const u1 = createUser('A');
const u2 = createUser('B');
```

Here the object shape is fixed → the engine optimizes.

But this is not good:

```js
const user = {};
user.name = 'A';
user.age = 25;
user.city = 'NY';
```

Adding properties sporadically will change the hidden class and may be de-opted.

## 🧠 Question 31

**ID**: js-031  
**Title**: What is the Execution Context in JavaScript and what are its main components?  
**Difficulty**: Hard  
**Category**: Execution Context

### Answer 📄

An Execution Context is an abstract environment where JavaScript code is evaluated and executed.

There are three types:

- Global Execution Context
- Function Execution Context
- Eval Execution Context

Each execution context consists of:

- Variable Environment
- Lexical Environment
- This Binding

The engine creates a new execution context whenever a function is invoked.

---

Example:

```js
var x = 10;

function foo() {
  var y = 20;
  console.log(x + y); // 30
}

foo();
```

## 🧠 Question 32

**ID**: js-032  
**Title**: What is the difference between the creation phase and execution phase of an execution context?  
**Difficulty**: Hard  
**Category**: Execution Context

### Answer 📄

During the creation phase:

- Memory is allocated for variables and functions.
- Variables declared with `var` are initialized with `undefined`.
- Function declarations are fully hoisted.

During the execution phase:

- Code runs line by line.
- Variables receive assigned values.
- Functions are executed.

---

Example:

```js
console.log(a); // undefined

var a = 5;
```

## 🧠 Question 33

**ID**: js-033  
**Title**: How does the Scope Chain work during variable resolution?  
**Difficulty**: Hard  
**Category**: Scope

### Answer 📄

The Scope Chain is a mechanism used to resolve variable access.

When a variable is referenced:

1. The engine checks the current scope.
2. If not found, it moves to the outer lexical scope.
3. This continues until reaching the global scope.
4. If not found, a ReferenceError is thrown.

This structure enables lexical scoping.

---

Example:

```js
const a = 1;

function outer() {
  const b = 2;

  function inner() {
    const c = 3;
    console.log(a, b, c); // 1 2 3
  }

  inner();
}

outer();
```

## 🧠 Question 34

**ID**: js-034  
**Title**: What is the difference between Lexical Scope and Dynamic Scope, and which one does JavaScript use?  
**Difficulty**: Medium  
**Category**: Scope

### Answer 📄

Lexical Scope means scope is determined by where a function is defined in the source code.

Dynamic Scope means scope is determined by how a function is called.

JavaScript uses Lexical Scope.

The scope of a function is fixed at definition time, not call time.

---

Example:

```js
function outer() {
  const x = 10;

  function inner() {
    console.log(x);
  }

  return inner;
}

const fn = outer();
fn(); // 10
```

## 🧠 Question 35

**ID**: js-035  
**Title**: What is a Closure in JavaScript and how does it relate to lexical scoping?  
**Difficulty**: Medium  
**Category**: Closures

### Answer 📄

A closure is created when a function remembers variables from its lexical scope even after the outer function has finished executing.

Closures are possible because JavaScript uses lexical scoping.

They allow functions to retain access to variables from their defining environment.

---

Example:

```js
function counter() {
  let count = 0;

  return function () {
    count++;
    return count;
  };
}

const increment = counter();

console.log(increment()); // 1
console.log(increment()); // 2
```

## 🧠 Question 36

**ID**: js-036  
**Title**: Why can closures cause memory leaks in certain situations?  
**Difficulty**: Hard  
**Category**: Memory & Performance

### Answer 📄

Closures can cause memory leaks when they retain references to large objects that are no longer needed.

If a closure keeps a reference alive, the garbage collector cannot free that memory.

Common causes include:

- Unremoved event listeners
- Long-running timers
- Cached data in closures

---

Example:

```js
function createHandler() {
  const bigData = new Array(1000000).fill('data');

  return function () {
    console.log(bigData.length);
  };
}

const handler = createHandler();
// bigData stays in memory as long as handler exists
```

To avoid this, only keep what is actually needed inside the closure:

```js
function createHandler() {
  const bigData = new Array(1000000).fill('data');
  const length = bigData.length; // extract only what's needed

  return function () {
    console.log(length); // bigData is no longer referenced
  };
}

const handler = createHandler();
```

## 🧠 Question 37

**ID**: js-037  
**Title**: What is the Temporal Dead Zone (TDZ) and how does it work with let and const?  
**Difficulty**: Medium  
**Category**: Scope

### Answer 📄

The Temporal Dead Zone is the time between entering a block scope and the actual declaration of a `let` or `const` variable.

During this period, accessing the variable results in a ReferenceError.

Unlike `var`, `let` and `const` are hoisted but not initialized.

---

Example:

```js
{
  console.log(a); // ReferenceError: Cannot access 'a' before initialization
  let a = 10;
}
```

## 🧠 Question 38

**ID**: js-038  
**Title**: How does block scope differ from function scope?  
**Difficulty**: Medium  
**Category**: Scope

### Answer 📄

Function scope means variables declared with `var` are scoped to the entire function.

Block scope means variables declared with `let` and `const` are scoped to the nearest block `{}`.

Block scope prevents accidental variable leakage outside conditional or loop blocks.

---

Example:

```js
if (true) {
  var x = 1;
  let y = 2;
}

console.log(x); // 1
console.log(y); // ReferenceError
```

## 🧠 Question 39

**ID**: js-039  
**Title**: What happens internally when a function is returned from another function?  
**Difficulty**: Hard  
**Category**: Closures

### Answer 📄

When a function is returned, its lexical environment is preserved if it references outer variables.

The engine keeps those variables in memory so the returned function can access them later.

This is the foundation of closures.

---

Example:

```js
function greet(name) {
  return function () {
    console.log('Hello ' + name);
  };
}

const sayHello = greet('Rasool');
sayHello(); // Hello Rasool
```

## 🧠 Question 40

**ID**: js-040  
**Title**: How does JavaScript handle variable lookup when multiple nested scopes exist?  
**Difficulty**: Hard  
**Category**: Scope

### Answer 📄

JavaScript resolves variables using the Scope Chain.

It searches from the innermost scope outward until it finds the variable.

If the variable does not exist in any scope, a ReferenceError is thrown.

This lookup process is determined at function definition time.

Example:

```js
const a = 'global';

function first() {
  const a = 'first';

  function second() {
    console.log(a);
  }

  second();
}

first(); // "first"
```
