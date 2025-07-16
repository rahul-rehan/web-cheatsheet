## 1. What is a property in a JavaScript object?

A **property** in a JavaScript object is a key-value pair where the key (also called a property name) is a string or symbol, and the value can be any JavaScript value (primitive, object, function, etc.). Properties represent the characteristics or attributes of the object.

## 2. How can you add, read, update, and delete properties from an object?

- **Add a property:**
```js
obj.newProp = 'value';
// or
obj['newProp'] = 'value';
```
- **Read a property:**

```js
let val = obj.existingProp;
// or
let val = obj['existingProp'];
```
- **Update a property:**

```js
obj.existingProp = 'newValue';
// or
obj['existingProp'] = 'newValue';
```
- **Delete a property:**

```js
delete obj.existingProp;
```
## 3. What are the differences between dot notation and bracket notation for accessing properties?

| Aspect               | Dot Notation                   | Bracket Notation                         |
|----------------------|-------------------------------|-----------------------------------------|
| Syntax               | `obj.propName`                 | `obj['propName']`                       |
| Property name type   | Only valid identifiers (no spaces, special chars) | Can use any string or variable as key  |
| Dynamic keys          | Cannot use variables directly | Can use variables or expressions        |
| Use cases            | Preferred for static, valid identifiers | Necessary for keys with spaces, special chars, or dynamic keys |

**Example:**

```js
const obj = { name: 'Alice', 'favorite color': 'blue' };
const key = 'name';

console.log(obj.name);         // Output: Alice
console.log(obj['favorite color']); // Output: blue
console.log(obj[key]);          // Output: Alice
console.log(obj.key);           // undefined, looks for property literally named 'key'
```
## 4. How can property names be dynamic or computed in object literals?

In JavaScript ES6 and later, you can use **computed property names** in object literals by enclosing an expression in square brackets `[]`. This expression is evaluated, and the result is used as the property name.

**Example:**

```js
const propName = 'age';
const person = {
  name: 'John',
  [propName]: 30,  // computed property name, results in 'age': 30
};

console.log(person.age); // Output: 30
```
## 5. Can property names be symbols in JavaScript?

Yes, property names in JavaScript can be **Symbols**. Symbols are unique and immutable primitive values that can be used as keys for object properties. Using Symbols as property keys helps avoid name collisions and creates properties that are not enumerable in normal loops.

**Example:**

```js
const sym = Symbol('id');
const user = {
  [sym]: 12345,
};

console.log(user[sym]); // Output: 12345
```
Properties keyed by Symbols are not included in `for...in` loops or `Object.keys()`, providing a way to create hidden or private-like object properties.