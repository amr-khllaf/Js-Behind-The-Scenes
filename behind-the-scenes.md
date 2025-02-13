---
title: How JavaScript Works Behind the Scenes
date: \today
---

# An High-Level "Overview" of JavaScript (Lecture 1)

## Basic Definition

### javascript is a high level, object-oriented programming , multi-paradigm language

---

# JavaScript: is a high-level, prototype-based object-oriented, multi-paradigm, dynamic language, interpreted or "just-in-time" compiled language with first-class functions, single-threaded, non-blocking event loop, and a garbage collector for automatic memory management.

## High-level:

It is a high-level language, which means it is closer to human language than machine language. It is easy to read and write. It is not necessary to remember the system architecture or manage memory.

## Garbage collector:

It is a garbage-collected language, which means it has a garbage collector that automatically allocates and deallocates memory. This means that you don't have to worry about memory management.

## Interpreted or "just-in-time" compiled language with first-class functions:

It is an interpreted language, which means that it is executed line by line. However, it is also a "just-in-time" compiled language with first-class functions, which means that it can be compiled into machine code at runtime. This makes it faster than other interpreted languages.

## Multi-paradigm:

It is a multi-paradigm language, which means that it supports different programming paradigms, such as object-oriented, functional, and imperative programming.

### Paradigm

An approach and mindset of structuring code, which will direct your coding style and technique.

1. Object-oriented programming (OOP)
2. Functional programming (FP)
3. Procedural programming (PP)

## Prototype-based object-oriented:

It is a prototype-based object-oriented language, which means that it uses prototypes to create objects. This is different from class-based object-oriented languages, such as Java or C++, which use classes to create objects.

## Dynamic language:

It is a dynamic language, which means that it is flexible and can change at runtime. This means that you can add or remove properties from objects, change the type of variables, and even change the behavior of functions.

## First-class functions:

It is a language with first-class functions, which means that functions are treated as first-class citizens. This means that functions can be assigned to variables, passed as arguments to other functions, and returned from other functions.

## Single-threaded:

It is a single-threaded language, which means that it can only execute one task at a time. This is different from multi-threaded languages, such as Java or C++, which can execute multiple tasks at the same time.

### Concurrency Model :

- how the JavaScript engine handles multiple tasks happening at the same time, we need that because JavaScript is single-threaded (This is mean that it can only execute one task at a time).
- So What about the long -running tasks? like fetching data from the server, or reading a file from the disk, or waiting for a user to click on a button, or waiting for a timer to finish.
- This wil be handled by using the `Event Loop` and `Callback Queue`.

## Non-blocking event loop:

It is a non-blocking event loop, which means that it can handle multiple tasks at the same time without blocking the main thread. This is done by using asynchronous functions, such as setTimeout or fetch, which allow the main thread to continue executing while waiting for the asynchronous function to finish.

---

# The JavaScript Engine and Runtime (Lecture 2)

## What is the JavaScript Engine?

- The JavaScript engine is a program that executes JavaScript code.
- It is responsible for parsing and executing JavaScript code.
- The most popular JavaScript engine is V8, which is used in "Google Chrome and Node.js".

## Js Engine Components:

1. Memory Heap: where the memory allocation happens.
2. Call Stack: where the code is executed.

### Memory Heap (Unstructured):

- This is where the memory allocation happens.
- This is where objects, variables, and function calls are stored.
- This is where the garbage collector works.
- The memory heap is a large region of memory that is used to store objects, variables, and function calls.

### Call Stack (Structured):

- This is where the code is executed Using the `Execution Context`.
- This is where the function calls are stored.
- This is where the function calls are executed in a last-in, first-out (LIFO) order.
- The call stack is a data structure that stores information about the active function calls in a program.

---

## How the code is Compiled to machine code?

### Compilation Vs Interpretation:

- Compilation: The entire source code is converted into machine code at once, and written to a binary (Portable) file that can be executed by a computer.

  - step 1 : Parsing the code : Converting the code into a data structure (AST) that the computer can understand.
    - Abstract Syntax Tree (AST) : A tree representation of the code that the computer can understand.
    - AST doesn't have a relation with the DOM tree.
  - step 2 : Compilation to a machine code (Portable file)
  - step 3 : Execution : Running the machine code directly (Program running)

- Interpretation: The source code is executed line by line.

  - step 1 : Parsing the code : Converting the code into a data structure that the computer can understand.
  - step 2 : Execution line by line

### Just-in-time compilation (JIT):

- The code is compiled to machine code before it is executed.
- The code is executed line by line.

- JavaScript is an interpreted language, but it is also a "just-in-time (JIT)" compiled language, which means that it can be compiled into machine code at runtime.

  - just-in-time compilation: The code is compiled into machine code at runtime, which makes it faster than other interpreted languages , ( This is mixed between compilation and interpretation)
  - 1. Parsing the code
  - 2. Compilation to machine code (Just-in-time)
  - Machine code isn't a portable file, it's a code that can be executed directly by the computer.

- After the Execution of the code, the machine code will be stored in the `Call Stack` and the `Memory Heap`and it will be optimized by the `Optimization Engine` to make it faster.
- This happens in the `V8 Engine` which is used in Google Chrome and Node.js.

- So this is mean the Js isn't an interpreted language, it's a compiled language, but it's compiled at runtime which is called "Just-in-time compilation".

![Modern JIT Compilation Of JS](./Pics/1.%20JIT.png)

---

## JS Runtime in Browsers:

- The JavaScript engine is not the only component of the JavaScript runtime in the browser.

- The JavaScript runtime in the browser consists of the following components:

  1. The JavaScript engine (V8 in Chrome).
  2. The Web APIs (DOM, AJAX, Timeout , Timers , Fetch API, ...).
  3. The Callback Queue.

     - The Callback Queue is a queue that stores the callbacks of asynchronous functions.
     - like : setTimeout, fetch, DOM events, click events, ...
     - The Callback Queue is also known as the Task Queue.

  4. The Event Loop.

     - The Event Loop is a loop that checks the Call Stack and the Callback Queue.
     - If the Call Stack is empty, it takes the first callback from the Callback Queue and pushes it to the Call Stack.

![JS Runtime in Browsers](./Pics/2.%20JS%20run%20Time%20In%20Browsers.png)

## JS Runtime in Node.js:

- The JavaScript runtime in Node.js is similar to the JavaScript runtime in the browser.

- The JavaScript runtime in Node.js consists of the following components:

  1. The JavaScript engine (V8 in Node.js).
  2. The Node APIs (File System, HTTP, OS, ...).
     - C++ bindings that allow JavaScript to interact with the operating system & Thread pool.
  3. The Callback Queue.
  4. The Event Loop.

![JS Runtime in Node.js](./Pics/3.%20JS%20run%20Time%20In%20NodeJs.png)

---

# Execution Context and The Call Stack (Lecture 3)

## How JavaScript code is executed?

- creation of the `Global Execution Context` and the `Global Object` (window object in the browser).
- Global execution context is created when the JavaScript engine starts executing the code.
- The global execution context is the first execution context that is created when the JavaScript engine starts executing the code.
- it's made for the global code (for top-level code , the code not inside any function) that is not inside any function.

## What is the Execution Context:

- Environment in which a piece of JavaScript is executed.

- Stores all the necessary information for the code to be executed

### Exactly one global execution context (EC) is created when the script is loaded

- Default EC for the code that is not inside any function (top-level code)

### One Execution Context is created for each function call

- Each function has its own execution context

- For Each function call, a new execution context is created and added to the top of the call stack.

- When the function returns, its execution context is removed from the call stack.

![Execution Context](./Pics/4.%20Execution%20Context.png)

---

## What is inside the Execution Context:

1. Variable Environment (VE)

   - let, const, var, function declarations
   - variables
   - function arguments
   - arguments object

2. Scope Chain
3. `this` keyword

- All of these are created during the "creation phase" of the execution context, which is happening before the Execution.

### Note about Arrow Functions:

- Arrow functions do not have their own `this` keyword, they use the `this` keyword of their parent scope.

- Arrow functions do not have their own `arguments` object, they use the `arguments` object of their parent scope.

![What is inside the Execution Context](./Pics/5.%20inside%20Execution%20Context.png)

## Simulate The Creation Phase:

- The creation phase is the phase in which the execution context is created and the necessary information is stored in the execution context.

- The creation phase consists of the following steps:

  1. Creation of the Variable Environment (VE).
  2. Creation of the Scope Chain.
  3. Determination of the value of the `this` keyword.

- The creation phase is happening before the execution of the code.

![Simulate The Creation Phase](./Pics/6.%20Simulate%20Execution%20Context.png)

---

## The Call Stack:

- The call stack is a data structure that stores information about the active function calls in a program.

- The call stack is a last-in, first-out (LIFO) data structure.

- The call stack is used to keep track of the active function calls in a program.

- When a function is called, its execution context is added to the top of the call stack.

- The Function that is at the top of the call stack is the one that is currently being executed.

- When a function returns, its execution context is removed from the top of the call stack.

### How would the Engine Know which function was being executed before the current function?

- The engine keeps track of the execution context of the function that called the current function.

- This is done by using the `Scope Chain`.

- The `Scope Chain` is a chain of execution contexts that are created when a function is called.

- The `Scope Chain` is used to keep track of the parent function of the current function.

- The `Scope Chain` is used to determine the value of the `this` keyword.

- The order of the execution never get lost because of the `Scope Chain`.

## ![How the Call Stack Works](./Pics/7.%20How%20CAll%20Stack%20Work.png)

### Explain The Pic :

- The `Global Execution Context` is created when the JavaScript engine starts executing the code.

- The `Global Execution Context` is added to the top of the call stack.

- The `Global Execution Context` is the first execution context that is created when the JavaScript engine starts executing the code.

- When a function is called, its execution context is added to the top of the call stack.

- The function that is at the top of the call stack is the one that is currently being executed.

- When a function returns, its execution context is removed from the top of the call stack.

- The function that was called before the current function is added to the top of the call stack.

- The `Scope Chain` is used to keep track of the parent function of the current function.

- The `Scope Chain` is used to determine the value of the `this` keyword.

---
