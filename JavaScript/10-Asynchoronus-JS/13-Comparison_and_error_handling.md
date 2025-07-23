## 1. How does `Promise.race()` differ from `Promise.all()`?

| Feature              | `Promise.race()`                            | `Promise.all()`                                  |
|----------------------|---------------------------------------------|--------------------------------------------------|
| Settles when         | **First** Promise settles (resolve or reject) | **All** Promises must resolve                   |
| Rejects when         | First Promise rejects                       | **Any** Promise rejects                          |
| Ignores others after | First settled Promise                       | Continues until all settle or any reject         |
| Use case             | Timeouts, canceling long tasks              | Aggregating results of all Promises              |

## 2. How does `Promise.race()` differ from `Promise.any()`?

| Feature              | `Promise.race()`                          | `Promise.any()`                                     |
|----------------------|-------------------------------------------|-----------------------------------------------------|
| Settles on           | First Promise to settle (resolve or reject) | First Promise to **resolve** only                  |
| Ignores rejections?  | No — will reject if first is rejected     | Yes — ignores rejections until one resolves        |
| Rejects when         | First rejected Promise settles first      | **All** Promises reject (with `AggregateError`)     |
| Use case             | Timeouts, abort scenarios                 | First successful result from multiple attempts      |

## 3. How can you handle errors in `Promise.race()`?

- You can handle errors in `Promise.race()` using a `.catch()` block or a `try...catch` inside an `async` function.
- Since `Promise.race()` settles with the **first fulfilled or rejected Promise**, your error handling must be ready for immediate rejection.

### Example:

```javascript
const fastReject = new Promise((_, reject) => setTimeout(() => reject("Failed fast"), 100));
const slowResolve = new Promise(resolve => setTimeout(() => resolve("Success"), 500));

Promise.race([fastReject, slowResolve])
  .then(result => {
    console.log("Resolved with:", result);
  })
  .catch(error => {
    console.error("Rejected with:", error); // Output: Rejected with: Failed fast
  });
```
## 4. What happens if all Promises in `Promise.race()` reject, but at different times?

- `Promise.race()` **settles as soon as the first Promise settles**, regardless of whether it resolves or rejects.
- If all Promises reject, the **first one to reject** determines the outcome.
- The other rejections are ignored by `Promise.race()` because it does **not wait** for all Promises once one settles.

### Example:

```javascript
const p1 = new Promise((_, reject) => setTimeout(() => reject("Error 1"), 100));
const p2 = new Promise((_, reject) => setTimeout(() => reject("Error 2"), 200));

Promise.race([p1, p2])
  .catch(error => {
    console.error("Race rejected with:", error); // Output: "Race rejected with: Error 1"
  });
```
## 5. Can you combine `Promise.race()` with `async/await`? Provide an example.

Yes, you can use `Promise.race()` with `async/await` to simplify syntax and improve readability. This is especially useful for implementing timeouts or cancellation logic.

### Example using `async/await` and `Promise.race()`:

```javascript
async function fetchWithTimeout(url, timeout = 3000) {
  const fetchPromise = fetch(url);

  const timeoutPromise = new Promise((_, reject) => 
    setTimeout(() => reject(new Error("Timeout exceeded")), timeout)
  );

  try {
    const response = await Promise.race([fetchPromise, timeoutPromise]);
    const data = await response.json();
    console.log("Fetched data:", data);
  } catch (error) {
    console.error("Request failed:", error.message);
  }
}

fetchWithTimeout("https://api.example.com/data");
```
#### In this example:

- The fetch request races against a timeout Promise.

- If the fetch takes too long, the timeout causes the race to reject first.

- This technique helps enforce maximum response time limits.

## Advanced and Best Practices
## 1. What are common use cases where `Promise.race()` is a better fit than `Promise.all()`?

- **Implementing timeouts**: Enforce a maximum wait time for async operations.
- **Handling user cancellation**: Let a user action cancel a long-running task.
- **Prioritizing fastest result**: Use the quickest available response (e.g., querying multiple endpoints or CDNs).
- **Fail-fast scenarios**: Abort operations immediately when the first failure occurs (though `Promise.all` also rejects on first failure, it waits on all to complete if handled improperly).

## 2. What precautions should be taken when using `Promise.race()` for timeouts?

- **Avoid unhandled rejections**: Promises that settle after the race ends may still reject, causing unhandled rejection warnings.
- **Abort ongoing tasks if possible**: Use `AbortController` (in fetch) or custom cancel tokens to stop unnecessary work.
- **Clean up resources**: Ensure any side effects from pending tasks are cleared if the timeout wins the race.

## 3. Can `Promise.race()` result in memory leaks or unhandled rejections if not managed properly?

Yes, it can.

- **Unmanaged Promises continue to run** after the race settles. If they reject later and are not caught, this may trigger **unhandled rejection warnings**.
- **Memory leaks** can occur if long-running tasks accumulate or hold resources unnecessarily.
- To avoid this:
  - Always attach `.catch()` to all Promises if they may reject.
  - Use abort mechanisms or time-based cleanup when possible.

## 4. How would you cancel or ignore other Promises once `Promise.race()` settles?

- JavaScript Promises are not cancelable by default, but you can:
  - Use **`AbortController`** (e.g., with `fetch`) to cancel requests.
  - Implement **custom cancel logic** in your own async functions.
  - Use **flags** or state variables to ignore results from slower Promises.

### Example using `AbortController`:

```javascript
const controller = new AbortController();

const fetchPromise = fetch("https://api.example.com/data", {
  signal: controller.signal
});

const timeoutPromise = new Promise((_, reject) => 
  setTimeout(() => reject(new Error("Timeout")), 3000)
);

Promise.race([fetchPromise, timeoutPromise])
  .then(res => res.json())
  .then(data => console.log(data))
  .catch(err => {
    controller.abort(); // Cancel fetch if timeout wins
    console.error("Error:", err.message);
  });
```
## 5. What’s a real-world scenario where using `Promise.race()` improves user experience or performance?

### Example: Improving UX with fast failover

Imagine you want to load user profile data from one of two replicated servers and use the one that responds first:

```javascript
const serverA = fetch("https://server-a.com/profile");
const serverB = fetch("https://server-b.com/profile");

Promise.race([serverA, serverB])
  .then(res => res.json())
  .then(data => displayProfile(data))
  .catch(error => showError("All servers failed"));
```
#### Benefits:
- Reduced latency: The fastest responding server wins, regardless of location or load.

- Improved reliability: If one server is slow or down, the other can still fulfill the request.

- Better user experience: The user gets their content quicker without knowing which server provided it.

#### This technique is particularly useful in:

- High-availability systems

- Load-balanced APIs

- Multi-CDN environments