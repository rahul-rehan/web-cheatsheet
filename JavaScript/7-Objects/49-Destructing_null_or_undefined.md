## 1. What happens if you try to destructure properties from `null` or `undefined`?

- Attempting to destructure from `null` or `undefined` throws a **TypeError** because these values cannot be converted to objects.

## 2. How can you safely destructure from a potentially `null` or `undefined` object?

- Use a **default fallback object** during destructuring to avoid errors.
- Use **default parameters** in function arguments to ensure an object is always present.

## 3. What is the best way to avoid runtime errors during destructuring from null objects?

- Provide a default empty object `{}` either directly in the destructuring assignment or as a function parameter default.

## 4. Provide an example of destructuring with a fallback object or default parameter.

```javascript
// Using fallback in destructuring
const data = null;

const { name = 'Unknown' } = data || {};

console.log(name); // Unknown

// Using default parameter in function
function greet({ name = 'Guest' } = {}) {
  console.log(`Hello, ${name}!`);
}

greet();              // Hello, Guest!
greet({ name: 'Amy' }); // Hello, Amy!
```