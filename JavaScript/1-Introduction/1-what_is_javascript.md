# JavaScript Interview Questions and Answers

## 1. What is JavaScript, and how is it different from Java?

**JavaScript** is a high-level, interpreted programming language primarily used to add interactivity and dynamic behavior to web pages.

### Differences from Java:
- **Purpose**: Java is used for general-purpose programming (e.g., backend, Android apps), while JavaScript is mostly for web front-end development.
- **Syntax & Architecture**: They have C-style syntax but very different object models and execution environments.
- **Execution**: Java code is compiled to bytecode and runs on the Java Virtual Machine (JVM). JavaScript is interpreted or JIT-compiled and runs in browsers or on Node.js.
- **Typing**: Java is statically typed; JavaScript is dynamically typed.

---

## 2. Is JavaScript a compiled or interpreted language?

JavaScript is traditionally **interpreted**, but modern engines like **V8 (used in Chrome and Node.js)** use **Just-In-Time (JIT) compilation** to improve performance.  
So, it's best described as **interpreted with JIT compilation**.

---

## 3. What type of programming language is JavaScript?

JavaScript is a **multi-paradigm** language. It supports:
- **Procedural programming** (e.g., using functions and loops)
- **Object-oriented programming** (via prototypes and ES6 classes)
- **Functional programming** (e.g., using higher-order functions, closures, immutability)

---

## 4. What is the role of JavaScript in web development?

JavaScript is used for:
- **Client-side scripting** to create interactive user interfaces (e.g., form validation, dynamic content)
- **Manipulating the DOM** (Document Object Model)
- **Handling events** (clicks, input, etc.)
- **Communicating with servers** via APIs (AJAX, Fetch)
- **Single-page applications (SPAs)** using frameworks like React, Angular, and Vue.js

---

## 5. What environments can JavaScript run in apart from browsers?

Apart from browsers, JavaScript can run in:
- **Node.js** – Server-side JavaScript runtime
- **Deno** – A modern secure JavaScript/TypeScript runtime
- **Mobile apps** (via React Native)
- **IoT devices** (e.g., Espruino, Tessel)
- **Desktop apps** (e.g., Electron)
- **Embedded systems and serverless functions** (e.g., AWS Lambda)

---

## 6. Is JavaScript single-threaded or multi-threaded? Explain with an example.

JavaScript is **single-threaded** by design due to its use of the **event loop**. This means it can only execute one piece of code at a time.

However, JavaScript can **handle asynchronous operations** (like API calls, timers) using:
- **Callbacks**
- **Promises**
- **Async/Await**
- **Web APIs + Event Loop**

### Example:
```javascript
console.log("Start");

setTimeout(() => {
  console.log("Inside setTimeout");
}, 1000);

console.log("End");
```

Output:
```javascript
Start  
End  
Inside setTimeout
```

Even though setTimeout is delayed, it doesn't block the main thread. JavaScript offloads it and continues executing, then returns to it via the event loop.

To achieve actual multi-threading, JavaScript uses:

Web Workers (in browsers)

Worker Threads (in Node.js)