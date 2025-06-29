## 1. What is the syntax of a ternary (`? :`) operator?

The ternary operator is a concise way to write simple `if-else` statements. The syntax is:

```javascript
condition ? expressionIfTrue : expressionIfFalse
```
- **condition**: The expression to evaluate.

- **expressionIfTrue**: The value or expression returned if the condition is `true`.

- **expressionIfFalse**: The value or expression returned if the condition is `false`.
## 2. Convert the following if-else block into a ternary:

```javascript
if (x > 10) {
  y = "big";
} else {
  y = "small";
}
```
### Converted using ternary operator:
```js
y = (x > 10) ? "big" : "small";
```
## 3. Can ternary operators be nested? Provide an example.

Yes, ternary operators can be nested to handle multiple conditions, though excessive nesting can hurt readability.

#### Example of nested ternary:

```javascript
let score = 75;

let grade = (score >= 90) ? "A"
          : (score >= 80) ? "B"
          : (score >= 70) ? "C"
          : (score >= 60) ? "D"
          : "F";

console.log(grade);  // Output: "C"
```
In this example, multiple conditions are checked using nested ternaries to assign a grade based on the score.
## 4. When should you avoid using ternary operators?

- **Avoid using ternary operators when the logic is complex or involves multiple nested conditions.**
  - Deeply nested ternaries reduce readability and make the code harder to understand and maintain.
- **Avoid using ternary operators for executing multiple statements.**
  - Ternary operators are best suited for simple, single expressions. For multiple lines of code, use traditional `if-else` blocks.
- **Avoid using ternaries when side effects are involved.**
  - If you need to perform actions like logging, modifying variables, or calling functions with side effects, prefer `if-else` for clarity.


## 5. What is the result of `false ? "yes" : "no"`?

The condition `false` evaluates to `false`, so the ternary operator returns the **expression after the colon**.

```javascript
false ? "yes" : "no"  // Returns "no"
