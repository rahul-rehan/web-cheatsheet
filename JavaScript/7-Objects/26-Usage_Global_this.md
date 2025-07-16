## 1. How do you define a global variable using `globalThis`?

You can define a global variable by assigning a property directly on `globalThis`. This makes the variable accessible globally across different environments.

```js
globalThis.myGlobalVar = 42;
console.log(myGlobalVar); // 42
```
## 2. Can you access existing global variables using `globalThis`?

Yes, all existing global variables and functions are properties of `globalThis`. You can access them directly through it.

```js
console.log(globalThis.parseInt === parseInt); // true
console.log(globalThis.Array === Array);       // true
```
## 3. Provide an example where `globalThis` is used inside a function or module

```js
function printGlobalVar() {
  if (globalThis.myGlobalVar !== undefined) {
    console.log('Global variable:', globalThis.myGlobalVar);
  } else {
    console.log('Global variable not defined');
  }
}

globalThis.myGlobalVar = 'Hello, global!';
printGlobalVar(); // Output: Global variable: Hello, global!
```
## 4. What is the output of `globalThis === window` in the browser?

```js
console.log(globalThis === window); // true
```
In a browser environment, `globalThis` and `window` refer to the same global object, so the comparison returns `true`.
## 5. How can `globalThis` be helpful in writing cross-platform JavaScript code?

`globalThis` provides a unified and standard way to access the global object across different JavaScript environments such as browsers, Node.js, and Web Workers. Instead of checking for environment-specific globals like `window`, `global`, or `self`, you can use `globalThis` to write code that runs consistently everywhere.

**Example:**

```js
// Set a global variable in any environment
globalThis.myGlobalValue = 42;

// Access the global variable
console.log(globalThis.myGlobalValue); // 42
```
This makes your code more portable and reduces environment-specific conditional checks.