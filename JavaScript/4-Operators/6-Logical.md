## 1. What are the three main logical operators in JavaScript?

- **Logical AND (`&&`)**  
- **Logical OR (`||`)**  
- **Logical NOT (`!`)**

---

## 2. How does the logical AND (`&&`) operator work?

- It returns the **first falsy operand** if any, otherwise the **last truthy operand**.
- Both operands are evaluated left to right.
- It is often used to check multiple conditions where **all must be true**.

Example:
```javascript
true && 'Hello';    // returns 'Hello' (both truthy, returns last)
false && 'Hello';   // returns false (first falsy value)
```
## 3. What will be the result of `true`?

The expression `true` itself evaluates to the boolean value **`true`**.

If used in a JavaScript context as a standalone value, it simply represents the boolean literal `true`.

For example:

```javascript
console.log(true);  // Output: true
```
## 4. What is short-circuit evaluation in logical expressions?

In logical expressions, evaluation stops as soon as the result is determined.

- For `&&` (AND), if the first operand is falsy, the whole expression is falsy, so the second operand is **not evaluated**.
- For `||` (OR), if the first operand is truthy, the whole expression is truthy, so the second operand is **not evaluated**.

This can be used for conditional execution or default values.

**Example:**

```javascript
false && someFunction();  // someFunction() is NOT called
true || someFunction();   // someFunction() is NOT called
```
## 5. How does JavaScript treat non-boolean values in logical expressions?

JavaScript uses **truthy** and **falsy** concepts when evaluating non-boolean values in logical expressions.

- **Truthy** values are treated as `true` in boolean contexts (e.g., non-empty strings, non-zero numbers, objects).
- **Falsy** values are treated as `false` (e.g., `false`, `0`, `""` (empty string), `null`, `undefined`, `NaN`).

Logical operators return one of the operands directly, not necessarily a boolean.

---

## 6. What will `null || "default"` evaluate to?

The expression `null || "default"` evaluates to `"default"`.

Explanation: Since `null` is falsy, the `||` operator returns the second operand `"default"`.

---

## 7. What is the result of `false && 0 && ""`?

The expression `false && 0 && ""` evaluates to `false`.

Explanation: The `&&` operator stops evaluation and returns the first falsy operand. Since `false` is falsy, it is returned immediately.

---

## 8. How can logical operators be used for default value assignments in JavaScript?

Logical OR (`||`) can be used to assign default values when the first value is falsy.

Example:

```javascript
const name = userInput || "Guest";
```
If `userInput` is falsy (e.g., `null`, `undefined`, or `""`), `name` will be assigned `"Guest"`.

Similarly, logical AND (`&&`) can be used for conditional execution:

```javascript
isLoggedIn && showDashboard();
```
`showDashboard()` runs only if `isLoggedIn` is truthy.