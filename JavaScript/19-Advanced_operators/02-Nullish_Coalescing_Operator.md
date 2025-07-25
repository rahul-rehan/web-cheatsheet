## 1. What is the nullish coalescing operator `??` in JavaScript?

The nullish coalescing operator (`??`) returns the right-hand side operand when the left-hand side operand is **null** or **undefined**. Otherwise, it returns the left-hand side operand. It is useful for providing default values only when dealing with `null` or `undefined`, and not other falsy values like `0`, `''`, or `false`.

**Example:**
```js
let name = null;
let defaultName = 'Guest';
console.log(name ?? defaultName); // Output: 'Guest'
```
## 2. What is the key difference between `??` and `||`?

- `??` (nullish coalescing) only considers **null** and **undefined** as "empty" values and returns the right operand only in those cases.
- `||` (logical OR) considers **all falsy values** (`false`, `0`, `''`, `null`, `undefined`, `NaN`) as "empty" and returns the right operand if the left is any falsy value.

**Example:**

```js
let count = 0;

console.log(count ?? 5); // Output: 0  (0 is not nullish, so ?? returns 0)
console.log(count || 5); // Output: 5  (0 is falsy, so || returns 5)
```
## 3. Provide an example where `??` operator is useful

The `??` operator is useful when you want to assign a default value only if a variable is `null` or `undefined`, but allow other falsy values like `0` or `''`.

```js
let userCount = 0;

// Using ?? to assign default only if userCount is null or undefined
let totalUsers = userCount ?? 10;

console.log(totalUsers); // Output: 0
```
Here, `userCount` is `0` (falsy but not nullish), so `??` returns `0` instead of the default `10`.
## 4. Can the `??` operator be chained? Give an example.

Yes, the `??` operator can be chained to evaluate multiple expressions from left to right, returning the first value that is not `null` or `undefined`.

```js
let a = null;
let b = undefined;
let c = "Hello";

let result = a ?? b ?? c ?? "Default";

console.log(result); // Output: "Hello"
```
Here, `a` and `b` are nullish (`null` and `undefined`), so the operator proceeds to `c`, which is `"Hello"`, the first non-nullish value returned.
## 5. What values are considered "nullish" in JavaScript?

In JavaScript, the values considered **nullish** are:

- `null`
- `undefined`

These are the only two values that the nullish coalescing operator (`??`) treats as nullish.

## 6. Can `??` be used in combination with other logical or conditional operators?

Yes, the `??` operator can be combined with other logical operators like `&&` and `||`, as well as conditional (`?:`) operators. 

**Important:** When combining `??` with `&&` or `||`, you must use parentheses to avoid syntax errors because of operator precedence.

**Example:**

```js
const a = null;
const b = false;
const c = a ?? (b && "Hello");
console.log(c); // Output: false
```
In this example, `a` is nullish, so the expression evaluates `b && "Hello"`. Since `b` is `false`, the result is `false`.

Using parentheses ensures correct evaluation order and prevents syntax errors.
## 7. Is it possible to use `??` inside an assignment? How?

Yes, you can use the nullish coalescing operator `??` inside an assignment to assign a default value when the left-hand side is `null` or `undefined`.

**Example:**
```js
let name = null;
let defaultName = "Guest";
let displayName = name ?? defaultName;  // displayName will be "Guest"
```
## 8. What happens if both sides of `??` are nullish?
If both sides of the `??` operator are nullish (`null` or `undefined`), the result of the expression will be `undefined`, since neither side provides a non-nullish value.

**Example:**

```js
let a = null;
let b = undefined;
let result = a ?? b;  // result is undefined
```