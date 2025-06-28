# Built-in Objects in JavaScript

## 1. What are built-in objects in JavaScript? Name at least five.

Built-in objects are standard objects provided by JavaScript to perform common tasks and represent data structures. Some examples include:

- `Object`
- `Array`
- `String`
- `Number`
- `Boolean`
- `Date`
- `Math`
- `RegExp`
- `Promise`

---

## 2. What is the purpose of the `Object` built-in object?

- The `Object` built-in object is the base for all JavaScript objects.
- It provides methods to create, manipulate, and interact with objects, such as:
  - Creating new objects
  - Defining or retrieving properties
  - Checking property existence
  - Managing prototypes and inheritance

---

## 3. What is the difference between `Array` and `Object` in JavaScript?

| Feature              | Array                                       | Object                                  |
|----------------------|---------------------------------------------|----------------------------------------|
| Data Structure       | Ordered list of values                       | Collection of key-value pairs           |
| Indexing             | Indexed by numeric keys (0, 1, 2, ...)      | Indexed by string or symbol keys        |
| Use Case             | Storing sequences, lists                     | Storing structured data with named keys |
| Built-in Methods     | `.push()`, `.pop()`, `.map()`, `.filter()`, etc. | `.hasOwnProperty()`, `.keys()`, `.values()`, etc. |
| Prototype            | Inherits from `Array.prototype`              | Inherits from `Object.prototype`        |

Arrays are specialized objects optimized for ordered data, while objects are general-purpose key-value stores.


## 4. What are some commonly used methods of the Array object?

Some frequently used `Array` methods include:

- `.push(element)` — Adds an element to the end of the array.
- `.pop()` — Removes and returns the last element.
- `.shift()` — Removes and returns the first element.
- `.unshift(element)` — Adds an element to the beginning.
- `.map(callback)` — Creates a new array by applying a function to each element.
- `.filter(callback)` — Creates a new array with elements that pass a test.
- `.reduce(callback, initialValue)` — Reduces the array to a single value.
- `.forEach(callback)` — Executes a function on each element.
- `.slice(start, end)` — Returns a shallow copy of a portion of the array.
- `.splice(start, deleteCount, items...)` — Adds/removes elements at a specified position.
- `.indexOf(value)` — Returns the first index of a value or -1 if not found.
- `.includes(value)` — Checks if an array contains a value.

---

## 5. What does the Date object represent and how do you create one?

- The `Date` object represents a single moment in time — including date and time information.
- You can create a `Date` object in several ways:

```javascript
const now = new Date();                     // Current date and time
const specificDate = new Date('2023-01-01'); // Date from a date string
const timestampDate = new Date(1672531200000); // Date from milliseconds since Jan 1, 1970 (Unix epoch)
const customDate = new Date(2023, 0, 1, 10, 30, 0); // Year, month (0-based), day, hours, minutes, seconds
```
## 6. How do you format or manipulate dates using the Date object?

- The `Date` object provides various methods for accessing and manipulating date/time components:

| Method                  | Description                             |
|-------------------------|-------------------------------------|
| `.getFullYear()`        | Gets the 4-digit year                |
| `.getMonth()`           | Gets the month (0-11)                |
| `.getDate()`            | Gets the day of the month (1-31)    |
| `.getHours()`           | Gets the hour (0-23)                 |
| `.getMinutes()`         | Gets the minutes (0-59)              |
| `.getSeconds()`         | Gets the seconds (0-59)              |
| `.setFullYear(year)`    | Sets the year                       |
| `.setMonth(month)`      | Sets the month (0-11)               |
| `.setDate(day)`         | Sets the day of the month           |
| `.toISOString()`        | Converts date to ISO string format   |
| `.toLocaleDateString()` | Converts date to locale-specific string |
| `.toString()`           | Converts date to a readable string   |

- Example: Formatting a date

    ```javascript
    const date = new Date();
    console.log(date.toLocaleDateString()); // e.g., '6/28/2025'
    console.log(date.toISOString());        // e.g., '2025-06-28T12:34:56.789Z'
    ```
- Manipulating dates by adding days:

    ```javascript
    const date = new Date();
    date.setDate(date.getDate() + 7);  // Adds 7 days
    console.log(date.toLocaleDateString());
    ```
## 7. What is the Math object used for? List some common methods.

The **Math** object in JavaScript provides properties and methods for mathematical constants and functions. It is a built-in object and not a constructor, so you use its methods directly.

**Common Math methods:**

- `Math.round(x)` – rounds x to the nearest integer.
- `Math.floor(x)` – rounds x down to the nearest integer.
- `Math.ceil(x)` – rounds x up to the nearest integer.
- `Math.abs(x)` – returns the absolute value of x.
- `Math.sqrt(x)` – returns the square root of x.
- `Math.pow(x, y)` – returns x raised to the power y.
- `Math.random()` – returns a random number between 0 (inclusive) and 1 (exclusive).
- `Math.max(a, b, ...)` – returns the largest of zero or more numbers.
- `Math.min(a, b, ...)` – returns the smallest of zero or more numbers.

---

## 8. What is the use of JSON object in JavaScript?

The **JSON** object provides methods for parsing JSON strings and converting JavaScript objects to JSON format. JSON (JavaScript Object Notation) is a lightweight data-interchange format that is easy for humans to read and write, and easy for machines to parse and generate.

Common uses of the JSON object:

- Serializing JavaScript objects into JSON strings for storage or network transmission.
- Parsing JSON strings back into JavaScript objects.

---

## 9. How do you convert an object to a JSON string and vice versa?

- **Convert object to JSON string:**  
  Use `JSON.stringify()` method.

  ```javascript
  const obj = { name: 'Alice', age: 25 };
  const jsonString = JSON.stringify(obj);
  console.log(jsonString);  // '{"name":"Alice","age":25}'
  ```
- **Convert JSON string to object:**
Use JSON.parse() method.

    ```javascript
    const jsonStr = '{"name":"Alice","age":25}';
    const obj = JSON.parse(jsonStr);
    console.log(obj.name);  // 'Alice'
    ```
## 10. What is the RegExp object and how is it used?

The **RegExp** object in JavaScript represents regular expressions, which are patterns used to match character combinations in strings. It is used for searching, replacing, and validating text.

You can create a RegExp object either by:

- Using a literal syntax:

  ```javascript
  const regex = /hello/i;  // 'i' flag for case-insensitive match
  ```
- Using the constructor:
    ```js
    const regex = new RegExp('hello', 'i');
    ```
**Common methods that use RegExp:**

- `regex.test(string)` — returns `true` if the pattern matches the string.
- `string.match(regex)` — returns an array of matches.
- `string.replace(regex, replacement)` — replaces matched text.

## 11. What does the Function object allow you to do in JavaScript?

The `Function` object allows you to create new functions dynamically in JavaScript.

Example:

```javascript
const sum = new Function('a', 'b', 'return a + b;');
console.log(sum(2, 3));  // Outputs: 5
```
This is useful for dynamic code generation, though it should be used carefully due to performance and security concerns (similar to `eval`).

## 12. How are wrapper objects like String, Number, and Boolean different from their primitive counterparts?

Primitive values like `'hello'`, `42`, and `true` are simple data types stored directly.

Wrapper objects like `new String('hello')`, `new Number(42)`, and `new Boolean(true)` are object instances that wrap these primitive values.

**Differences:**

- Primitives are immutable and more efficient.
- Wrapper objects provide additional methods and properties.
- JavaScript automatically wraps primitives with their corresponding wrapper objects when methods are accessed (this is called *boxing*).

**Example:**

```javascript
const strPrimitive = 'hello';
const strObject = new String('hello');

console.log(typeof strPrimitive); // "string"
console.log(typeof strObject);    // "object"
```
Generally, it's recommended to use primitives rather than wrapper objects to avoid unexpected behavior.
## 13. What is the use of the Error object? How do you create custom errors?

The **Error** object in JavaScript is used to represent runtime errors. It provides a standard way to create, throw, and catch errors in your code.

- It contains useful properties like:
  - `message`: description of the error.
  - `name`: type of error (e.g., "Error", "TypeError").
  - `stack`: stack trace showing where the error occurred.

**Creating and throwing an error:**

```javascript
throw new Error('Something went wrong!');
```
**Creating custom errors:**

You can create custom error types by extending the built-in Error class:

```javascript
class ValidationError extends Error {
  constructor(message) {
    super(message);
    this.name = 'ValidationError';
  }
}

throw new ValidationError('Invalid input!');
```
This helps you differentiate error types and handle them appropriately.
## 14. How do built-in objects differ from user-defined objects?

- **Built-in objects** are provided by the JavaScript environment and include objects like `Array`, `Date`, `Math`, `Error`, `RegExp`, and `Object`.

    - They have predefined properties and methods.

    - They are optimized and maintained by the JavaScript engine.

    - You typically use them to perform common tasks (manipulate arrays, dates, math operations, etc.).

- **User-defined objects** are created by developers to model data and behavior specific to their application.

    - Created via object literals, constructor functions, or classes.

    - Their properties and methods are defined by the user.

    - Serve as the backbone for custom data structures and abstractions.

