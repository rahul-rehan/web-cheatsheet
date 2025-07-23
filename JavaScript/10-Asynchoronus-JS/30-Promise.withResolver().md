## 1. What is Promise.withResolvers() in JavaScript?

`Promise.withResolvers()` is a proposed (but not yet standard) utility method that creates a new Promise along with its associated resolve and reject functions, exposing them externally. This allows manual control over when the Promise is settled.

## 2. What type of value does Promise.withResolvers() return?

It returns an object containing both the Promise itself and the functions to resolve or reject it.

## 3. What are the properties of the object returned by Promise.withResolvers()?

The returned object typically has three properties:

- `promise`: The newly created Promise instance.
- `resolve`: A function that, when called, resolves the Promise with a given value.
- `reject`: A function that, when called, rejects the Promise with a given reason (error).

Example structure:

```js
{
  promise: Promise,
  resolve: function,
  reject: function
}
```
## 4. Provide a basic example of using Promise.withResolvers()

```js
const { promise, resolve, reject } = Promise.withResolvers();

promise.then(value => {
  console.log("Resolved with:", value);
}).catch(error => {
  console.error("Rejected with:", error);
});

// Manually resolve the promise later
resolve("Success!");

// Or to reject:
// reject(new Error("Failure"));
```
## 5. How is Promise.withResolvers() different from manually creating a Promise and saving resolve/reject?

- **Promise.withResolvers()** provides a concise and standardized way to create a Promise along with its `resolve` and `reject` functions in a single step.
- When manually creating a Promise, you need to write boilerplate code to capture the `resolve` and `reject` callbacks inside the Promise executor, like this:

```js
let resolve, reject;
const promise = new Promise((res, rej) => {
  resolve = res;
  reject = rej;
});
```
- `Promise.withResolvers()` abstracts this pattern and returns an object containing the promise and its associated resolver functions, making the code cleaner and less error-prone.