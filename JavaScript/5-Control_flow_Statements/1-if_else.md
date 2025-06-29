# JavaScript `if` Statement Basics

## 1. What is the syntax of a basic `if` statement in JavaScript?

The basic syntax of an `if` statement in JavaScript is:

```javascript
if (condition) {
  // code to execute if the condition is true
}
```
### Condition in JavaScript `if` Statement

- **Condition**: An expression that is evaluated as `true` or `false`.

- If the condition evaluates to `true`, the block of code inside the `{}` is executed.

- If it evaluates to `false`, the code block is skipped.

#### Example:
```javascript
let age = 20;
if (age >= 18) {
  console.log("You are an adult.");
}
```
## 2. What is the difference between `if` and `if-else` statements?

| **Feature**       | **`if` Statement**                                 | **`if-else` Statement**                                      |
|-------------------|----------------------------------------------------|---------------------------------------------------------------|
| **Basic Behavior**| Executes a block of code if condition is `true`    | Executes one block if `true`, another if `false`              |
| **Else Block**    | Not included                                       | Includes an `else` block for when the condition is `false`    |
### Example of `if`:
```javascript
if (score > 50) {
  console.log("You passed!");
}
```
### Example of `if-else`:
```javascript
if (score > 50) {
  console.log("You passed!");
} else {
  console.log("You failed.");
}
```
## 4. How does JavaScript evaluate conditions in an `if-else if-else` chain?

JavaScript evaluates each condition in an `if-else if-else` chain **from top to bottom**. As soon as it finds a condition that evaluates to `true`, it executes the associated block and **skips the rest** of the chain.

#### Syntax:
```javascript
if (condition1) {
  // code if condition1 is true
} else if (condition2) {
  // code if condition2 is true
} else {
  // code if none of the above conditions are true
}
```
**Example:**
```js
let temperature = 30;

if (temperature > 35) {
  console.log("It's very hot!");
} else if (temperature > 25) {
  console.log("It's warm.");
} else {
  console.log("It's cool.");
}
```
- In this example, if `temperature` is `30`, the second condition is true (`temperature > 25`), so `"It's warm."` is printed.

- The third block (`else`) is ignored once a true condition is found.
## 5. What happens if none of the `if` or `else if` conditions are met and there’s no `else`?

If none of the `if` or `else if` conditions evaluate to `true` and there is **no `else` block**, then **no code is executed** from that conditional structure.

#### Example:
```javascript
let number = 5;

if (number > 10) {
  console.log("Greater than 10");
} else if (number < 0) {
  console.log("Less than 0");
}
// No `else` block
```
In this case, since `number` is 5, and it doesn't satisfy either condition, nothing is printed.
## 6. Can `if` conditions use assignment instead of comparison accidentally? What are the consequences?

Yes, it is a common mistake to use an **assignment operator (`=`)** instead of a **comparison operator (`==` or `===`)** in `if` conditions.

#### Example of accidental assignment:
```javascript
let isReady = false;

if (isReady = true) {  // assignment instead of comparison!
  console.log("Ready!");
}
```
In this example, `isReady = true` assigns the value `true` to the variable `isReady`, and since the assignment itself evaluates to `true`, the `if` block runs. This can lead to unexpected behavior and bugs.

#### Consequences:
- The value `true` is assigned to `isReady`, and then the condition evaluates to `true`, so the block will **always execute**.
- This can lead to **unexpected behavior and bugs**, especially when you meant to check for equality.

#### Best Practice:
- Use `===` for **strict comparison** to avoid unintended type coercion.
- Consider enabling **linters** or **IDE warnings** to help catch such mistakes early in development.
## 7. Explain truthy and falsy values in the context of `if` conditions

In JavaScript, `if` conditions do not always require a boolean (`true` or `false`). Instead, the condition expression is **coerced** to a boolean when evaluated. This means that values are interpreted as either **truthy** or **falsy**.

- **Truthy values**: Values that are considered `true` when converted to a boolean.
- **Falsy values**: Values that are considered `false` when converted to a boolean.

#### Common Falsy Values:
- `false`
- `0`
- `""` (empty string)
- `null`
- `undefined`
- `NaN`

#### Examples:
```javascript
if ("hello") {
  console.log("This is truthy!"); // Runs because non-empty strings are truthy
}

if (0) {
  console.log("Won't run"); // 0 is falsy, so this block is skipped
}
```
## 8. How can nested if-else statements be simplified for readability?

Nested `if-else` statements can become hard to read and maintain when deeply nested. Here are some ways to simplify them:

#### 1. Use `else if` chains instead of nested `if` inside `else`:

Flatten the logic to avoid multiple levels of indentation.

```javascript
// Nested
if (condition1) {
  // code
} else {
  if (condition2) {
    // code
  }
}

// Simplified using else if
if (condition1) {
  // code
} else if (condition2) {
  // code
}
```
#### 2. Use early returns (in functions):

Return early when a condition is met to avoid deep nesting.
```js
function check(value) {
  if (value < 0) {
    return "Negative";
  }
  if (value === 0) {
    return "Zero";
  }
  return "Positive";
}
```
#### 3. Use switch statements for multiple discrete values:
```js
switch (value) {
  case 0:
    console.log("Zero");
    break;
  case 1:
    console.log("One");
    break;
  default:
    console.log("Other");
}
```
#### 4. Break complex conditions into separate functions:

This improves clarity and modularity.

