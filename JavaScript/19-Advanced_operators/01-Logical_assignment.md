## 1. What are logical assignment operators in JavaScript?

Logical assignment operators combine logical operations (`&&`, `||`, `??`) with assignment. They allow for more concise expressions when assigning a value based on a condition.

There are three main logical assignment operators:
- `&&=`: Logical AND assignment
- `||=`: Logical OR assignment
- `??=`: Nullish coalescing assignment

These operators assign a new value to a variable only when a logical condition is met.

## 2. What does the `&&=` operator do?

The `&&=` operator assigns a value to a variable only if the current value is truthy.

```js
let isActive = true;
isActive &&= "active";
console.log(isActive); // "active"
```
#### If the left-hand side is falsy, the assignment does not occur:

```js
let isReady = false;
isReady &&= "ready";
console.log(isReady); // false
```
#### It’s equivalent to:

```js
if (isActive) {
  isActive = "active";
}
```
## 3. What does the ||= operator do?
The ||= operator assigns a value only if the variable is falsy.

```js
let userName = "";
userName ||= "Guest";
console.log(userName); // "Guest"
```
Equivalent to:

```js
if (!userName) {
  userName = "Guest";
}
```
## 4. What does the ??= operator do?
The ??= operator assigns a value only if the variable is null or undefined.

```js
let count = null;
count ??= 1;
console.log(count); // 1
```
It won’t assign if the value is 0 or an empty string (which are falsy but not nullish):

```js
let score = 0;
score ??= 100;
console.log(score); // 0
```
Equivalent to:

```js
if (count === null || count === undefined) {
  count = 1;
}
```
## 5. Code Example: Using the `&&=` Operator in JavaScript

The `&&=` operator assigns a new value to a variable **only if** the current value is truthy.

#### Example:

```js
let isAuthenticated = true;

// Assign "User123" only if isAuthenticated is truthy
isAuthenticated &&= "User123";

console.log(isAuthenticated); // Output: "User123"
```
#### Another Example (Falsy Case):
```js
let isAdmin = false;

// Since isAdmin is falsy, the assignment does not occur
isAdmin &&= "SuperAdmin";

console.log(isAdmin); // Output: false
```
#### Equivalent to:
```js
if (isAuthenticated) {
  isAuthenticated = "User123";
}
```
This operator is useful for simplifying conditional assignments based on a truthy check.
## 6. Code Example: Using the `||=` Operator in JavaScript

The `||=` (logical OR assignment) operator assigns a value to a variable **only if** the current value is falsy.

#### Example:

```js
let username = "";

// Assign "Guest" only if username is falsy (empty string is falsy)
username ||= "Guest";

console.log(username); // Output: "Guest"
```
#### Another Example (Truthy Case):
```js
let email = "user@example.com";

// Since email is truthy, the assignment does not happen
email ||= "default@example.com";

console.log(email); // Output: "user@example.com"
```
#### Equivalent to:
```js
if (!username) {
  username = "Guest";
}
```
This operator is useful for providing default values when variables are uninitialized or falsy.
## 7. Code Example: Using the `??=` Operator in JavaScript

The `??=` (nullish coalescing assignment) operator assigns a value to a variable **only if** the current value is `null` or `undefined`.

#### Example 1: Assigning a default value if variable is null

```js
let config = null;

// Assign default config only if config is null or undefined
config ??= { theme: "light", layout: "grid" };

console.log(config); // Output: { theme: "light", layout: "grid" }
```
Example 2: Value is already defined (not nullish)
```js
let options = false;

// `false` is not null or undefined, so the assignment does not happen
options ??= true;

console.log(options); // Output: false
```
#### Equivalent to:
```js
if (config === null || config === undefined) {
  config = { theme: "light", layout: "grid" };
}
```
✅ Use ??= when you want to provide a fallback only if the variable is null or undefined, but not other falsy values like false, 0, or "".
## 8. How does short-circuiting work with logical assignment operators?

Logical assignment operators (`&&=`, `||=`, `??=`) utilize short-circuiting based on the value of the left-hand operand:

- `x &&= y` — Assigns `y` to `x` only if `x` is truthy.
- `x ||= y` — Assigns `y` to `x` only if `x` is falsy.
- `x ??= y` — Assigns `y` to `x` only if `x` is `null` or `undefined` (nullish).

This allows concise expressions that conditionally update variables based on their current value.

## 9. What are the differences between `||=`, `&&=`, and `??=`?

| Operator | Description                   | Assigns if...                 | Short-circuits when...  |
|----------|-------------------------------|-------------------------------|--------------------------|
| `||=`    | Logical OR assignment          | Left-hand side is falsy       | Left is truthy           |
| `&&=`    | Logical AND assignment         | Left-hand side is truthy      | Left is falsy            |
| `??=`    | Nullish coalescing assignment  | Left-hand side is `null` or `undefined` | Left is not nullish      |

## 10. When should you use `??=` instead of `||=`?

Use `??=` when you only want to assign a value if the variable is `null` or `undefined`, but **not** for other falsy values like `0`, `''` (empty string), or `false`.

**Example:**

```js
let count = 0;
count ||= 10;  // count becomes 10 (undesired if 0 is a valid value)
count ??= 10;  // count stays 0 (correct behavior if 0 is meaningful)
```
`??=` is safer when you want to preserve valid falsy values while still providing defaults for missing (`null` or `undefined`) values.
## 11. Can logical assignment operators be used with non-boolean values? Explain with an example.

Yes, logical assignment operators (`&&=`, `||=`, and `??=`) **can be used with non-boolean values**. These operators don't require boolean operands; instead, they operate based on the **truthiness**, **falsiness**, or **nullishness** of the left-hand operand.

#### Example:

```js
let title = '';
title ||= 'Untitled';
console.log(title); // Output: "Untitled"
```
In this case, `''` (empty string) is **falsy**, so `||=` assigns `'Untitled'` to `title`.

Another example using `??=`:

```js
let count = 0;
count ??= 5;
console.log(count); // Output: 0
```
Here, `0` is falsy, but not nullish, so `??=` does not assign `5`.

These examples demonstrate that logical assignment operators can operate on any type of value, as long as you're aware of how JavaScript evaluates their truthiness or nullishness.