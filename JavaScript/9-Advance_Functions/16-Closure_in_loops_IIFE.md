## 1. What is an IIFE (Immediately Invoked Function Expression)?

- An **IIFE** is a JavaScript function that is **defined and executed immediately** after its creation.
- It is typically written as a function expression wrapped in parentheses, followed by another set of parentheses to invoke it immediately.
- IIFEs create a new scope, helping to avoid polluting the global scope and to preserve variables within that scope.

#### Example of an IIFE:

```javascript
(function() {
  console.log('This runs immediately!');
})();
```
## 2. How does wrapping a loop body with an IIFE help preserve the loop variable’s value?

- Wrapping the loop body inside an IIFE creates a **new function scope** for each iteration.
- The current loop variable value is passed as an argument to the IIFE, which **captures and preserves that value** within its own scope.
- This ensures that each closure inside the loop gets its **own copy** of the loop variable, avoiding the issue where all closures share the same variable.
- As a result, when closures (like callbacks) execute later, they access the **correct value** of the loop variable corresponding to the iteration when the closure was created.
## 3. Rewrite a loop using an IIFE that prints 0, 1, 2 with `setTimeout`

```javascript
for (var i = 0; i < 3; i++) {
  (function(currentValue) {
    setTimeout(function() {
      console.log(currentValue); // Logs: 0, 1, 2
    }, 100);
  })(i); // Pass current value of i to the IIFE
}
```
- The IIFE is immediately invoked with the current value of `i` on each iteration.

- This creates a new scope for each iteration where `currentValue` holds the value of `i` at that time.

- Each `setTimeout` callback then logs the correct value corresponding to its iteration.
## 4. What are the pros and cons of using IIFE for this use case?

#### Pros:
- **Preserves loop variable value:** IIFEs create a new scope for each iteration, capturing the current value of the loop variable.
- **Avoids polluting global scope:** Variables inside the IIFE are scoped locally.
- **Compatible with pre-ES6 environments:** Works well in older JavaScript versions without block scoping (`let`/`const`).

#### Cons:
- **Verbosity:** Adds extra syntax, making code less readable compared to newer constructs.
- **More complex to understand:** For beginners, IIFEs can be confusing.
- **Less intuitive:** Modern alternatives offer clearer semantics.

## 5. Is IIFE still needed in modern ES6+ code? Why or why not?

- **Generally, no.**
- ES6 introduced `let` and `const`, which provide **block scoping**.
- Using `let` in loops creates a new binding per iteration, **eliminating the need for IIFEs** to capture loop variables.

#### Example with `let`:

```javascript
for (let i = 0; i < 3; i++) {
  setTimeout(function() {
    console.log(i); // Logs: 0, 1, 2
  }, 100);
}
```
- This code is simpler and easier to read.

- IIFEs are mostly used now for compatibility with older JavaScript environments or specific advanced patterns.