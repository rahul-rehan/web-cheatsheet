## 1. Can you break a line between parameters and the arrow (`=>`)?

- **No**, you should **not break the line** directly between the parameters and the `=>` symbol.
- Doing so causes a syntax error because JavaScript expects the `=>` to immediately follow the parameter list.

#### Incorrect (will throw an error):

```javascript
const sum = (a, b)
=> a + b;
```
## 2. What is a common syntax error when using line breaks in arrow functions?

- A common mistake is placing a **line break between the parameter list and the arrow (`=>`)**, which leads to a syntax error.

#### Incorrect:

```javascript
const multiply = (x, y)
=> x * y; // ❌ SyntaxError: Unexpected token =>
```
## 3. What is the correct way to format a multi-line arrow function for readability?

- Use **curly braces `{}`** to define a block body.
- Include an explicit **`return`** statement if the function returns a value.
- Always keep the **arrow `=>` on the same line** as the parameter list.

#### Example:

```javascript
const calculateTotal = (price, tax) => {
  const total = price + price * tax;
  return total;
};
```
- This approach ensures clarity and avoids common syntax issues with line breaks.