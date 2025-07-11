## 1. How can memoization optimize recursive functions?

Memoization is an optimization technique that **caches the results** of expensive function calls and returns the cached result when the same inputs occur again. In recursive functions, it helps avoid **recomputing the same subproblems** multiple times, significantly improving performance—especially for functions with overlapping subproblems like Fibonacci.


## 2. Write a memoized version of a recursive Fibonacci function.

```javascript
function fibonacciMemo(n, memo = {}) {
  if (n === 0) return 0;
  if (n === 1) return 1;

  if (memo[n]) return memo[n];               // Return cached result if available

  memo[n] = fibonacciMemo(n - 1, memo) + fibonacciMemo(n - 2, memo);
  return memo[n];
}
```
## 3. Can you write a recursive function to deeply clone a nested object?

```javascript
function deepClone(obj) {
  if (obj === null || typeof obj !== 'object') {
    return obj; // Return the value if obj is not an object
  }

  if (Array.isArray(obj)) {
    // Handle arrays
    return obj.map(item => deepClone(item));
  }

  // Handle objects
  const clone = {};
  for (const key in obj) {
    if (obj.hasOwnProperty(key)) {
      clone[key] = deepClone(obj[key]);
    }
  }
  return clone;
}
```
This function recursively clones all nested objects and arrays, creating a fully independent copy without shared references.
## 4. What is mutual recursion? Provide an example.

**Mutual recursion** occurs when two or more functions call each other recursively, rather than a single function calling itself. This creates a cycle of function calls between them.

#### Example:

```javascript
function isEven(n) {
  if (n === 0) return true;
  return isOdd(n - 1);
}

function isOdd(n) {
  if (n === 0) return false;
  return isEven(n - 1);
}

console.log(isEven(4)); // true
console.log(isOdd(7));  // true
```
Here, `isEven` calls `isOdd` and `isOdd` calls `isEven` until the base case is reached.
## 5. How does JavaScript handle recursive calls in asynchronous functions (e.g., with `setTimeout`)?

- When recursion involves asynchronous functions like `setTimeout`, each recursive call is **scheduled to run after the current call stack is cleared**.

- Instead of immediate recursive calls stacking up on the call stack, `setTimeout` places the next call in the **event queue**, allowing the call stack to unwind first.

- This means asynchronous recursion is **non-blocking** and **prevents stack overflow**, as each call happens in a new event loop cycle.

#### Example:

```javascript
function asyncCountdown(n) {
  if (n <= 0) {
    console.log("Done!");
    return;
  }
  console.log(n);
  setTimeout(() => asyncCountdown(n - 1), 1000); // Schedule next call asynchronously
}

asyncCountdown(5);
```
- Here, each recursive call to `asyncCountdown` is delayed and executed asynchronously, avoiding deep call stack buildup.