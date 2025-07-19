## 1. How do you define an arrow function with multiple parameters?

- Use parentheses around the parameters, followed by the arrow `=>`.

#### Example:

```javascript
const multiply = (a, b) => a * b;
console.log(multiply(2, 3)); // Output: 6
```
## 2. How do you define an arrow function with a single parameter?

- You can omit the parentheses if the arrow function has only **one parameter** and does not use default values or destructuring.

#### Example:

```javascript
const square = x => x * x;
console.log(square(4)); // Output: 16
```
## 3. Can you omit parentheses when an arrow function has only one parameter?

- **Yes**, you can omit parentheses when the arrow function has exactly **one parameter** and:
  - It does **not** use a **default value**
  - It does **not** use **destructuring**

#### Valid example:

```javascript
const greet = name => `Hello, ${name}!`;
```
#### Invalid without parentheses (requires parentheses due to default parameter):
```javascript
const showInfo = (name = "Guest") => `Welcome, ${name}`;
```
## 4. How do you define an arrow function with no parameters?

- You **must use empty parentheses** `()` when defining an arrow function that takes no parameters.

#### Example:

```javascript
const sayHello = () => console.log("Hello!");
sayHello(); // Output: Hello!
```
## 5. When must you use parentheses in an arrow function parameter list?

You must use parentheses in the following cases:

- **No parameters:**  
  ```javascript
  const sayHi = () => console.log("Hi!");
  ```
- Multiple parameters:

    ```javascript
    const add = (a, b) => a + b;
    ```
- Default parameter values:

    ```javascript
    const greet = (name = "Guest") => `Hello, ${name}`;
    ```
- Destructured parameters:

    ```javascript
    const display = ({ name }) => console.log(name);
    ```
