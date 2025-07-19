## 1. Why does using `var` inside a loop with closures lead to unexpected output?

- Variables declared with `var` have **function scope**, not block scope.
- When used inside a loop, `var` does **not create a new binding for each iteration**.
- Closures inside the loop all capture the **same single variable**, which gets updated on every iteration.
- As a result, when the closures execute later, they all reference the **final value** of the loop variable instead of the value during their creation.

## 2. Why do all the `setTimeout` callbacks inside a loop using `var` print the same value?

- Because the `var` variable is shared across all iterations, each `setTimeout` callback captures the **same variable reference**.
- By the time the callbacks run, the loop has completed and the variable holds its **last updated value**.
- Therefore, all callbacks print this same final value instead of their respective iteration values.

#### Example:

```javascript
for (var i = 0; i < 3; i++) {
  setTimeout(function() {
    console.log(i); // Logs: 3, 3, 3
  }, 100);
}
```
## 3. How does the value of the loop variable behave when accessed inside a closure using `var`?

- The loop variable declared with `var` is **function-scoped**, meaning there is only one shared variable for the entire loop.
- Closures created inside the loop **capture a reference to this single variable**, not its value at each iteration.
- As a result, when the closure executes, it accesses the **current value** of the loop variable at that time, which will be the **final value after the loop ends**.

#### Example:

```javascript
for (var i = 0; i < 3; i++) {
  setTimeout(function() {
    console.log(i); // Outputs: 3, 3, 3
  }, 100);
}
```
- Here, all closures log `3` because `i` has the final value `3` after the loop completes, and they all share the same variable.
### How to fix this?
- Use `let` instead of `var` to get block-scoped variables that create a new binding on each iteration:

```javascript
for (let i = 0; i < 3; i++) {
  setTimeout(function() {
    console.log(i); // Logs: 0, 1, 2
  }, 100);
}
```
- Alternatively, create an IIFE to capture the variable at each iteration (pre-ES6):

```javascript
for (var i = 0; i < 3; i++) {
  (function(j) {
    setTimeout(function() {
      console.log(j); // Logs: 0, 1, 2
    }, 100);
  })(i);
}
```