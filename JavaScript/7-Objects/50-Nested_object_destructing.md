## 1. How do you destructure properties from a nested object?

You can destructure nested objects by using nested curly braces `{}` matching the structure of the object.

## 2. Can you use default values for nested properties?

Yes, you can assign default values to nested properties in the destructuring pattern to handle missing or `undefined` values.

## 3. Provide an example of nested destructuring with default values.

```javascript
const user = {
  name: 'John',
  address: {
    city: 'New York',
    zip: undefined
  }
};

const {
  name,
  address: {
    city = 'Unknown City',
    zip = '00000'
  } = {}
} = user;

console.log(name); // John
console.log(city); // New York
console.log(zip);  // 00000 (default applied)
```
#### In this example:

- `city` is taken from the object normally.

- `zip` is `undefined` in the object, so the default `'00000'` is used.

- The `address = {}` default ensures destructuring does not fail if `address` is missing.
## 4.Can you rename nested properties during destructuring?

Yes, you can rename nested properties by specifying the property name followed by a colon and the new variable name inside the nested destructuring pattern.

#### Example:

```javascript
const user = {
  profile: {
    firstName: 'Alice',
    lastName: 'Smith'
  }
};

const { profile: { firstName: fName, lastName: lName } } = user;

console.log(fName); // Alice
console.log(lName); // Smith
```
## 5. What happens if any part of the nested path is undefined?

- If any intermediate property in the nested path is `undefined` or `null`, attempting to destructure deeper properties will throw a **TypeError** because you cannot destructure properties from `undefined` or `null`.
- To avoid this error, you can provide default empty objects `{}` at each level that might be missing.

#### Example:

```javascript
const user = {};

// This will throw an error:
// const { profile: { firstName } } = user; 

// Safe way with defaults:
const { profile: { firstName } = {} } = user || {};

console.log(firstName); // undefined (no error)
```