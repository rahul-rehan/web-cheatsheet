## 1. How do you return a value from a function?

You use the `return` statement followed by the value or expression you want to return. This ends the function execution and sends the value back to the caller.

#### Example:

```javascript
function add(a, b) {
  return a + b;
}

const result = add(2, 3);  // result is 5
```
## 2. What happens if there is no return statement in a function?

If a function does not have a `return` statement, it returns `undefined` by default after executing all its code.

#### Example:

```javascript
function greet(name) {
  console.log(`Hello, ${name}!`);
}

const result = greet("Alice");  
console.log(result);  // Output: undefined
```
## 3. Can you return multiple values from a function? How?

JavaScript functions can only return **one value**, but you can return **multiple values by grouping them inside an object or an array**.

#### Returning multiple values using an object:

```javascript
function getUser() {
  return {
    name: "Alice",
    age: 25,
  };
}

const user = getUser();
console.log(user.name);  // Output: Alice
console.log(user.age);   // Output: 25
```
#### Returning multiple values using an array:
```javascript
function getCoordinates() {
  return [10, 20];
}

const [x, y] = getCoordinates();
console.log(x);  // Output: 10
console.log(y);  // Output: 20
```
## 4. What is the difference between `return` and `console.log()`?

- **`return`**:  
  - Ends function execution and **sends a value back** to where the function was called.  
  - The returned value can be **stored, used, or passed** to other functions.

- **`console.log()`**:  
  - Outputs information to the **browser's console** (used for debugging).  
  - Does **not affect** the flow of the program or return anything to the caller.

#### Example:

```javascript
function add(a, b) {
  return a + b;           // Returns the result
}

function logSum(a, b) {
  console.log(a + b);     // Logs the result to the console
}

const result = add(2, 3);   // result = 5
logSum(2, 3);               // Console Output: 5
```
## 5. Can a function return an object or another function?

Yes, in JavaScript, a function can return:

- An **object**
- Another **function**

#### Returning an object:

```javascript
function createUser(name, age) {
  return {
    name: name,
    age: age,
  };
}

const user = createUser("Alice", 25);
console.log(user);  // Output: { name: 'Alice', age: 25 }
```
#### Returning a function:
```javascript
function multiplier(factor) {
  return function(number) {
    return number * factor;
  };
}

const double = multiplier(2);
console.log(double(5));  // Output: 10
```