## 1. What is object destructuring in JavaScript?

Object destructuring is a syntax that allows you to unpack properties from objects into distinct variables in a concise and readable way.

## 2. How do you destructure properties from an object into variables?

You use curly braces `{}` on the left side of the assignment to specify the property names you want to extract from the object.

## 3. Provide an example of basic object destructuring.

```javascript
const person = {
  name: 'Alice',
  age: 30,
  city: 'New York'
};

const { name, age } = person;

console.log(name); // Alice
console.log(age);  // 30
```
## 4. Can you rename variables while destructuring an object? How?

Yes, you can rename variables by using the syntax `propertyName: newVariableName` inside the destructuring pattern.

#### Example:

```javascript
const person = { name: 'Alice', age: 30 };

const { name: firstName, age: years } = person;

console.log(firstName); // Alice
console.log(years);     // 30
```
## 5. What happens if a destructured property does not exist in the object?

- If the property is missing, the destructured variable is assigned `undefined` by default.
- You can provide a default value to avoid getting `undefined`.

#### Example:

```javascript
const person = { name: 'Alice' };

const { age = 25 } = person;

console.log(age); // 25 (default value)
```
