## 1. How can you use await with Promise.all()?

You can use `await` with `Promise.all()` to run multiple promises in parallel and wait for all of them to resolve before proceeding. This improves performance compared to awaiting each promise sequentially.

```js
async function fetchData() {
  const [result1, result2, result3] = await Promise.all([
    fetch(url1),
    fetch(url2),
    fetch(url3)
  ]);
  // process results
}
```
## 2. How can you retry a failed await operation in an async function?

You can implement retries by wrapping the awaited operation inside a loop or recursive function with a try/catch block. If an error occurs, you retry the operation a specified number of times before failing.

```js
async function fetchWithRetry(url, retries = 3) {
  for (let i = 0; i < retries; i++) {
    try {
      const response = await fetch(url);
      if (!response.ok) throw new Error('Network error');
      return await response.json();
    } catch (error) {
      if (i === retries - 1) throw error; // rethrow after last attempt
    }
  }
}
```
## 3. Can you mix async/await and Promise chaining? Provide an example.

Yes, you can mix async/await with Promise chaining in the same codebase. This allows you to use the readability of async/await while still leveraging `.then()` and `.catch()` where appropriate.

### Example:

```js
async function getUserData(userId) {
  try {
    const user = await fetchUser(userId); // async/await style
    return user;
  } catch (error) {
    console.error('Error fetching user:', error);
    throw error;
  }
}

getUserData(1)
  .then(user => {
    // Promise chaining style
    return fetchPosts(user.id);
  })
  .then(posts => {
    console.log('User posts:', posts);
  })
  .catch(error => {
    console.error('Error fetching posts:', error);
  });
```
## 4. Can async functions be recursive? Provide a use case.

Yes, async functions can be recursive. A common use case is when performing asynchronous tree traversal or fetching paginated data where each call depends on the result of the previous async call.

**Example use case:** Recursively fetching nested comments or categories from an API.

```js
async function fetchComments(commentId) {
  const comment = await fetchCommentById(commentId);
  if (comment.replies.length === 0) return comment;

  comment.replies = await Promise.all(
    comment.replies.map(replyId => fetchComments(replyId))
  );
  return comment;
}
```
## 5. What is the return type of an async arrow function?

An async arrow function always returns a **Promise**, even if you return a direct value.

Example:

```js
const asyncFunc = async () => 42;

asyncFunc().then(value => {
  console.log(value); // Logs 42
});
```
## 6. Can you use async/await inside a loop? What are the implications?

Yes, you can use async/await inside a loop, but it affects how the asynchronous operations are executed:

- **Using `await` inside a `for` loop** runs the asynchronous operations **sequentially**, waiting for each to complete before starting the next one. This can lead to slower overall execution if the operations are independent.

Example of sequential execution:

```js
for (const item of items) {
  await asyncOperation(item);
}
```
- To run multiple async operations in parallel, you should collect the Promises first and then `await` them together, for example using `Promise.all()`:

```js
const promises = items.map(item => asyncOperation(item));
await Promise.all(promises);
```
#### Implications:
- Sequential loops are simpler but can be slower.

- Parallel execution is faster but requires handling of all Promises together.

- Be cautious with error handling when running Promises in parallel.

## Common Pitfalls and Best Practices
## 1. Common mistakes developers make when using async/await

- **Using `await` inside loops without parallelizing**: This causes asynchronous operations to run sequentially, leading to slower performance.
- **Not handling errors properly**: Forgetting to use `try...catch` around awaited calls can cause unhandled rejections.
- **Mixing `async/await` with `.then()` chains inconsistently**, making code harder to read and debug.
- **Forgetting that `async` functions always return a Promise**, which may affect how results are handled.
- **Not considering concurrency limits** when running many async operations in parallel, possibly overwhelming resources.

## 2. Why might using await inside a loop lead to performance issues?

Using `await` inside a loop causes each asynchronous operation to wait for the previous one to complete before starting. This **sequential execution** can significantly slow down the overall process, especially if the operations are independent and could run concurrently.

## 3. How can you execute async operations concurrently using await?

To run async operations concurrently, start all Promises first without awaiting them immediately, then wait for all to complete using `Promise.all()`:

```js
const promises = items.map(item => asyncOperation(item));
const results = await Promise.all(promises);
```
This approach launches all async tasks in parallel and waits for all to settle, improving performance compared to sequential awaits.
## 4. Best practices when working with async/await in production code

- **Always use `try...catch` blocks** around `await` calls to handle errors gracefully.
- **Avoid unnecessary sequential awaits** by running independent async tasks in parallel with `Promise.all()`.
- **Limit concurrency** when running many parallel operations to prevent resource exhaustion (use libraries like `p-limit`).
- **Return or propagate errors** properly so they can be logged or handled upstream.
- **Use meaningful error messages** and consider custom error types for better debugging.
- **Avoid mixing async/await and `.then()` chains inconsistently** to maintain code clarity.
- **Test asynchronous code thoroughly**, including error cases and edge conditions.
- **Use linters and static analysis tools** that support async/await patterns to catch common mistakes early.
- **Document async functions clearly** to show that they return Promises.

## 5. How can you globally catch unhandled errors from async functions?

- In Node.js, listen for the `'unhandledRejection'` event on the `process` object:

  ```js
  process.on('unhandledRejection', (reason, promise) => {
    console.error('Unhandled Rejection at:', promise, 'reason:', reason);
    // Log the error, clean up resources, or exit the process if necessary
  });
  ```
- In browsers, listen for the `'unhandledrejection'` event on the `window` object:

    ```js
    window.addEventListener('unhandledrejection', event => {
    console.error('Unhandled rejection:', event.reason);
    // Optionally prevent default logging or perform cleanup
    });
    ```
These global handlers help catch errors that were not properly handled with `try...catch` or `.catch()`, improving application stability and debugging.