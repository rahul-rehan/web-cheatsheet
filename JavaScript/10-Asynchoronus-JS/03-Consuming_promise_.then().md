## 1. What is the `.then()` method used for?

The `.then()` method is used to specify what should happen **when a Promise is fulfilled**. It allows you to define a **callback function** that will be executed once the Promise resolves successfully.

It also enables **Promise chaining**, where you can perform a sequence of asynchronous operations in order.

## 2. How many arguments does `.then()` accept? What do they represent?

The `.then()` method accepts **up to two arguments**:

1. **onFulfilled** (required):  
   A function that is called when the Promise is fulfilled. It receives the resolved value as its argument.

2. **onRejected** (optional):  
   A function that is called if the Promise is rejected. It receives the error or reason for rejection.

### Example:

```javascript
myPromise.then(
  value => console.log("Fulfilled with:", value),
  error => console.error("Rejected with:", error)
);
```
However, it's often better practice to use `.catch()` for handling rejections separately for better readability.
## 3. How does chaining `.then()` work?

Chaining `.then()` works by returning a **new Promise** from each `.then()` call. The return value from one `.then()` is automatically passed as the input to the next `.then()` in the chain.

This pattern allows you to execute multiple asynchronous operations in a clean and readable sequence.

### Example:

```javascript
doSomething()
  .then(result => {
    console.log("Step 1:", result);
    return doSomethingElse(result);
  })
  .then(nextResult => {
    console.log("Step 2:", nextResult);
    return "Final Result";
  })
  .then(final => {
    console.log("Step 3:", final);
  })
  .catch(error => {
    console.error("Error occurred:", error);
  });
```
#### Key Points:
- Each `.then()` returns a new Promise, even if you return a simple value.

- If a `.then()` returns a Promise, the next `.then()` waits for it to resolve.

- A single `.catch()` at the end can catch errors from any part of the chain.

## 4. Provide an example of chaining multiple `.then()` calls

You can chain multiple `.then()` calls to perform a series of operations one after another, especially when working with asynchronous logic.

### Example:

```javascript
const fetchData = () => {
  return new Promise((resolve) => {
    setTimeout(() => resolve(10), 1000); // Simulates async operation
  });
};

fetchData()
  .then(data => {
    console.log("Step 1:", data); // 10
    return data * 2;
  })
  .then(result => {
    console.log("Step 2:", result); // 20
    return result + 5;
  })
  .then(final => {
    console.log("Step 3:", final); // 25
  })
  .catch(error => {
    console.error("Error:", error);
  });
```
## 5. Can `.then()` return a value to the next `.then()` in the chain?

Yes, `.then()` can **return a value** to the next `.then()` in the chain.

- If you return a **non-Promise value**, it is automatically wrapped in a resolved Promise and passed to the next `.then()`.
- If you return a **Promise**, the next `.then()` waits for that Promise to resolve and receives its resolved value.

### Example:

```javascript
Promise.resolve(5)
  .then(num => {
    return num + 3; // returns 8 to the next .then()
  })
  .then(result => {
    console.log(result); // Output: 8
  });
```
This ability to return values (or Promises) makes `.then()` chaining useful for creating sequential asynchronous workflows.