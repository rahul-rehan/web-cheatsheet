## 1. What does the `break` statement do inside loops or switch statements?

The `break` statement **immediately exits** the nearest enclosing loop or switch statement, stopping further iterations or case checks.

---

## 2. What does the `continue` statement do, and how is it different from `break`?

- The `continue` statement **skips the rest of the current loop iteration** and moves to the next iteration of the loop.
- Unlike `break`, which exits the loop entirely, `continue` only skips ahead within the loop.

---

## 3. Example where `continue` is useful for skipping even numbers in a loop:

```javascript
for (let i = 0; i <= 10; i++) {
  if (i % 2 === 0) {
    continue;  // Skip even numbers
  }
  console.log(i);  // Prints only odd numbers: 1, 3, 5, 7, 9
}
```
## 4. Can you use `break` or `continue` outside of loops or switch statements?

No, both `break` and `continue` statements **can only be used inside loops or `switch` statements**. Using them outside of these structures will result in a syntax error.

## 5. What happens if `break` is used in a nested loop?

When `break` is used inside a nested loop, it **only exits the innermost loop** where it is called. The outer loops continue to execute normally.

#### Example:
```javascript
for (let i = 1; i <= 3; i++) {
  for (let j = 1; j <= 3; j++) {
    if (j === 2) {
      break;  // Exits the inner loop only
    }
    console.log(`i=${i}, j=${j}`);
  }
}
```
**Output:**
```ini
i=1, j=1
i=2, j=1
i=3, j=1
```
The inner loop stops when `j === 2`, but the outer loop continues to the next iteration.