## 1. What is the `Promise.any()` method in JavaScript?

- `Promise.any()` is a method that takes an iterable of Promises and returns a single Promise.
- It resolves as soon as **any one of the input Promises is fulfilled**.
- If **all Promises are rejected**, it rejects with an `AggregateError` containing all rejection reasons.
- It is the logical opposite of `Promise.all()`, which fails if any Promise fails.

## 2. What type of argument does `Promise.any()` accept?

- `Promise.any()` accepts an **iterable** (typically an array) of:
  - **Promises**, or
  - **Non-Promise values** (which are treated as immediately resolved Promises).

## 3. What does `Promise.any()` return when at least one Promise is fulfilled?

- It returns a new Promise that:
  - **Resolves** with the **value of the first fulfilled Promise** in the iterable.
  - **Ignores all rejections** unless every single Promise rejects.
- The result is the value of the **first successful** Promise.

### Example:

```javascript
const p1 = Promise.reject("Error A");
const p2 = Promise.resolve("Success B");
const p3 = Promise.resolve("Success C");

Promise.any([p1, p2, p3])
  .then(result => {
    console.log("Resolved with:", result); // Output: "Resolved with: Success B"
  })
  .catch(error => {
    console.error("All promises were rejected:", error);
  });
```
## 4. What happens when the first fulfilled Promise is returned?

- As soon as **any one Promise fulfills**, `Promise.any()`:
  - **Resolves immediately** with that Promise’s fulfillment value.
  - **Ignores all other Promises**, even if they fulfill or reject later.
- Other Promises continue executing in the background but **do not affect the outcome** of `Promise.any()`.

## 5. In what order does `Promise.any()` evaluate the Promises?

- Promises in the iterable are **started immediately and concurrently**.
- `Promise.any()` does **not guarantee evaluation order** — it only resolves with the **first Promise that fulfills**, regardless of its position in the array.
- The **fastest fulfilled Promise wins**, not necessarily the first one in the list.
