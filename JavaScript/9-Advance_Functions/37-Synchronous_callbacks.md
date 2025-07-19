## 1. What is a Synchronous Callback?

A **synchronous callback** is a function passed as an argument to another function that is executed immediately within the calling function's execution flow. The calling function waits for the callback to complete before continuing.

## 2. Example of a Synchronous Callback Using `Array.prototype.map`

```javascript
const numbers = [1, 2, 3, 4];

const doubled = numbers.map(function(num) {
  return num * 2;
});

console.log(doubled); // Output: [2, 4, 6, 8]
```
In this example, the callback function is invoked synchronously for each element in the array during the execution of `map`.
## 3. Example of a Synchronous Callback Using Array.prototype.forEach
```javascript
const fruits = ['apple', 'banana', 'cherry'];

fruits.forEach(function(fruit) {
  console.log(fruit);
});

// Output:
// apple
// banana
// cherry
```
Here, the callback is called synchronously for each item in the array.
## 4. How are synchronous callbacks executed in the JavaScript event loop?

Synchronous callbacks are executed **immediately** within the current call stack during the execution of the function that receives them. They run **before** the event loop continues to the next task or processes any asynchronous events. Because they are part of the current execution context, the event loop does not move on until the synchronous callback finishes.

## 5. Are synchronous callbacks blocking or non-blocking? Why?

Synchronous callbacks are **blocking** because the JavaScript engine waits for them to complete before moving on to the next line of code or task. While a synchronous callback runs, the event loop is effectively paused, meaning no other code (including asynchronous callbacks) can execute until the synchronous callback finishes.
## 6. Can a synchronous callback throw errors directly into the caller function?

Yes, a synchronous callback can throw errors directly into the caller function because it executes within the same call stack. Any error thrown inside the callback will propagate up to the caller unless it is caught.

## 7. How can you handle exceptions in synchronous callbacks?

You can handle exceptions in synchronous callbacks using a `try...catch` block either inside the callback itself or around the function that invokes the callback. This ensures that errors are caught and managed gracefully without crashing the program.

```javascript
function executeCallback(cb) {
  try {
    cb();
  } catch (error) {
    console.error("Error caught:", error);
  }
}

executeCallback(() => {
  throw new Error("Oops!");
});
```