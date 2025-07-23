## 1. What does `Promise.any()` return if all Promises are fulfilled?

- If all Promises are fulfilled, `Promise.any()`:
  - **Resolves with the value of the first one that fulfills** (based on timing, not array order).
  - Other fulfilled Promises are ignored.
- It behaves the same as when only one Promise fulfills — it resolves with the **first fulfillment**.

## 2. Does the order of Promises matter when they are all fulfilled?

- **No**, the order of Promises in the array does **not** affect which one `Promise.any()` resolves with.
- It resolves with the **first Promise to actually fulfill**, which depends on how quickly each one completes.

## 3. Provide an example where all Promises are fulfilled and `Promise.any()` returns the first one.

```javascript
const p1 = new Promise(resolve => setTimeout(() => resolve("One"), 300));
const p2 = new Promise(resolve => setTimeout(() => resolve("Two"), 100));
const p3 = new Promise(resolve => setTimeout(() => resolve("Three"), 200));

Promise.any([p1, p2, p3])
  .then(result => {
    console.log("Resolved with:", result); // Output: "Resolved with: Two"
  })
  .catch(error => {
    console.error("All promises rejected:", error);
  });
```
- In this example, all Promises fulfill, but `p2` fulfills first after 100ms.

- Therefore, `Promise.any()` resolves with `"Two"`.