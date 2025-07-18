## 1. How can you dynamically create an object from a single key-value pair in JavaScript?

You can use **computed property names** in object literals to dynamically create an object from a key-value pair. This is useful when the key is stored in a variable and you want to use it as the object's property.

## 2. Provide a code example to convert a key-value pair into an object.

```javascript
const key = "name";
const value = "Alice";

const obj = {
  [key]: value
};

console.log(obj); // Output: { name: 'Alice' }
```
This approach is concise and leverages ES6+ syntax to dynamically assign property names at runtime.
## 3. What method can you use to build an object from an array of key-value pairs?

You can use the **`Object.fromEntries()`** method to build an object from an array of key-value pairs. Each element in the array should itself be an array with two elements: a key and a value.

## 4. What is the output of `Object.fromEntries([['name', 'John']])`?

```javascript
Object.fromEntries([['name', 'John']])
// Output: { name: 'John' }
```
This creates an object with one property: `name` with the value `'John'`.
## 5. How do `Object.entries()` and `Object.fromEntries()` work together?

`Object.entries()` and `Object.fromEntries()` are complementary methods in JavaScript that allow conversion between objects and arrays of key-value pairs.

- **`Object.entries(object)`**:  
  Converts an object into an array of `[key, value]` pairs.

- **`Object.fromEntries(array)`**:  
  Converts an array of `[key, value]` pairs back into an object.

#### Example:

```javascript
const user = { name: 'Alice', age: 25 };

// Convert object to entries
const entries = Object.entries(user);
// [['name', 'Alice'], ['age', 25]]

// Convert entries back to object
const reconstructed = Object.fromEntries(entries);
// { name: 'Alice', age: 25 }
```
This transformation is useful when you want to perform array operations like `map`, `filter`, or `reduce` on object data and then reconstruct the object.
## 6. Can you use a computed key when building an object programmatically?

Yes, you can use a computed key when building an object using square brackets `[]` to evaluate the expression at runtime.

#### Example:
```javascript
const key = 'username';
const obj = {
  [key]: 'Alice'
};

console.log(obj); // { username: 'Alice' }
```
This is especially useful when you need to dynamically assign keys based on variables or expressions.
## 7. What is the best way to convert a Map to a plain object?

The most straightforward and efficient way to convert a `Map` to a plain JavaScript object is by using the `Object.fromEntries()` method.

#### Example:
```javascript
const map = new Map([
  ['name', 'Alice'],
  ['age', 25]
]);

const obj = Object.fromEntries(map);

console.log(obj); // { name: 'Alice', age: 25 }
```
Why this works:
- `Object.fromEntries()` takes an iterable of key-value pairs (like a `Map`) and constructs a new object from them.

- It's concise and avoids manual iteration.

## Best Practices and Applications
## 1. When should you use computed properties instead of static property names?

You should use computed properties when:
- The property name is not known until runtime.
- You want to dynamically generate keys based on variables or expressions.
- You are working with data structures that require flexible or user-defined keys.

#### Example:
```javascript
const key = 'username';
const user = {
  [key]: 'john_doe'
};
```
## 2. What are the advantages of using computed properties in dynamic data structures?

- **Dynamic Key Generation:** You can compute property names at runtime using variables or expressions, making your objects more flexible.
- **Improved Code Reusability:** Enables reuse of logic for generating keys rather than hardcoding property names.
- **Support for Complex Structures:** Useful when dealing with user-generated content, configuration objects, or API responses where keys vary.

## 3. What are potential risks or mistakes when using dynamic property names?

- **Reduced Readability:** Computed property names can make code harder to read and understand, especially with complex expressions.
- **Runtime Errors:** Typos or incorrect expressions can lead to unexpected keys or behavior that’s hard to debug.
- **Property Overwrites:** If the same computed key is used more than once, it may unintentionally overwrite existing properties.
- **Debugging Difficulty:** Dynamic keys may not appear clearly in stack traces or logs, complicating debugging.
## 4. How can computed properties help in localization or configuration-driven code?

- **Dynamic Key Mapping:** Computed properties allow you to generate property names based on locale or configuration settings, enabling flexible data structures.
- **Internationalization (i18n):** Useful for setting language-specific content or labels dynamically (e.g., `obj[localeKey] = translation`).
- **Dynamic Configurations:** Helps build objects based on runtime settings like user roles, feature flags, or environment variables.

**Example:**
```js
const lang = 'en';
const translations = {
  [lang]: 'Hello',
  ['fr']: 'Bonjour',
};
console.log(translations.en); // "Hello"
```
## 5. Are computed property names supported in all modern JavaScript engines?

Yes, computed property names are supported in all modern JavaScript engines. They were introduced in **ES6 (ECMAScript 2015)** and are now widely adopted.

#### Supported environments include:

- **Modern browsers**: Chrome, Firefox, Safari, Edge, and Opera (latest versions)
- **Server-side**: Node.js (from version 4+)
- **JavaScript runtimes**: Deno and others supporting ES6+

Computed properties are safe to use in any environment that supports ES6 or later.
