## 1. Can a generator delegate to another generator? How?

Yes, a generator can delegate to another generator using the `yield*` expression. This allows the delegating generator to yield all values from the delegated generator seamlessly.

## 2. What is the purpose of the yield* expression? Provide an example.

- The `yield*` expression delegates the yield operations to another iterable or generator.
- It effectively "forwards" values from the delegated generator to the caller.

**Example:**

```javascript
function* generatorA() {
  yield 1;
  yield 2;
}

function* generatorB() {
  yield* generatorA(); // Delegates to generatorA
  yield 3;
}

for (const value of generatorB()) {
  console.log(value); // Outputs: 1, 2, 3
}
```
## 3. Can you use generators with Promises? How?

Yes, generators can be used with Promises to write asynchronous code in a synchronous style. A generator can yield Promises, and a runner function (like `co` or a custom implementation) can handle the Promise resolution and resume the generator with the resolved value.

**Example:**

```javascript
function* asyncGenerator() {
  const data = yield fetch('https://api.example.com/data').then(res => res.json());
  console.log(data);
}

function run(generator) {
  const iterator = generator();

  function step(nextF) {
    let next;
    try {
      next = nextF();
    } catch (e) {
      return Promise.reject(e);
    }
    if (next.done) {
      return Promise.resolve(next.value);
    }
    return Promise.resolve(next.value).then(
      v => step(() => iterator.next(v)),
      e => step(() => iterator.throw(e))
    );
  }

  return step(() => iterator.next());
}

run(asyncGenerator);
```
## 4. How do libraries like Redux-Saga use generators?

Libraries like **Redux-Saga** use generator functions to manage complex asynchronous side effects in Redux applications. Generators allow writing asynchronous flows in a synchronous, linear style by yielding effects (like API calls, delays, or dispatching actions) which the middleware interprets and executes. This makes the control flow easier to read, test, and maintain compared to deeply nested callbacks or Promises.

## 5. Are generator functions synchronous or asynchronous by default?

Generator functions are **synchronous** by default. When you call a generator function, it returns an iterator immediately without executing the function body. The function’s execution is paused and only progresses when `.next()` is called on the iterator. Asynchronous behavior can be introduced by yielding Promises and managing them with helper functions or middleware, but generators themselves do not inherently provide asynchronous execution.

## Best Practices and Pitfalls
## 1. What are the limitations of using generators?

- Generators are **synchronous** by default and require extra handling to work with asynchronous code.
- They can add complexity if misused, especially for simple iteration tasks.
- Error handling inside generators can be tricky.
- Debugging can be harder due to their paused/resumed execution model.
- Not as widely understood or used compared to async/await or Promises.

## 2. What is the difference between generators and async functions?

| Aspect                 | Generators                      | Async Functions                   |
|------------------------|--------------------------------|---------------------------------|
| Execution              | Synchronous pause/resume       | Asynchronous, returns Promises  |
| Syntax                 | `function*` with `yield`       | `async function` with `await`   |
| Use case               | Custom iteration, lazy evaluation | Simplified async flow control   |
| Return value           | Iterator object                | Promise resolving to a value    |
| Error handling         | Via `throw()` method           | Try/catch with async/await      |

## 3. When should you prefer generators over other iteration methods?

- When implementing **custom iterators** with complex logic.
- For **lazy evaluation** of data sequences to improve performance.
- When you need **pause/resume** capabilities within iteration.
- In libraries or frameworks that benefit from generator-based control flows (e.g., Redux-Saga).
- When you want to delegate iteration to other iterables via `yield*`.

## 4. How does the generator protocol relate to the iterator protocol?

- The **generator protocol** is a special case of the iterator protocol.
- Generators return an **iterator object** with a `next()` method.
- They comply with the iterator protocol by returning `{ value, done }` from `next()`.
- Additionally, generators support `.return()` and `.throw()` methods to control flow and error handling, extending basic iterator capabilities.

## 5. Can a generator function be recursive? What are the considerations?

- Yes, a generator function **can be recursive**.
- Recursion should be carefully managed to avoid **stack overflows**.
- Recursive generators can use `yield*` to delegate to themselves or other generators.
- Useful for traversing recursive data structures like trees or graphs lazily.
- Must handle termination conditions properly to avoid infinite loops.
