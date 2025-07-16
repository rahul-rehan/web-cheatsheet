## 1. What is the object property initializer shorthand in JavaScript?

The object property initializer shorthand is a syntax feature that allows you to create object properties using variable names directly, without repeating the key-value pair when the property name and the variable name are the same.

## 2. How does the shorthand improve code readability and conciseness?

- **Reduces repetition**: You don’t need to repeat the variable name for both the key and the value.
- **Improves readability**: Makes the code cleaner and easier to understand at a glance.
- **Simplifies object creation**: Especially useful in function returns and configurations.


## 3. Provide an example of using object property shorthand.

```javascript
const name = "Alice";
const age = 30;

// Without shorthand
const user1 = {
  name: name,
  age: age
};

// With shorthand
const user2 = {
  name,
  age
};

console.log(user2); // { name: 'Alice', age: 30 }
```
## 4. Can you use shorthand when the variable name and property name differ?

No, object property shorthand only works when the variable name and the property name are the same. If the names differ, you must use the full key-value syntax:

```javascript
const username = "Alice";

// ❌ Not allowed
const user1 = { name: username }; // ✅ This is correct, not shorthand
```
## 5. What happens if the property name is duplicated in shorthand?

If a property is defined more than once in an object (whether using shorthand or not), the **last defined value takes precedence** and overwrites the earlier one.

#### Example:

```javascript
const name = "Alice";

const user = {
  name: "Bob",
  name // shorthand for `name: "Alice"` — this overwrites "Bob"
};

console.log(user.name); // Output: "Alice"
```
## 6. When should you avoid using object property shorthand?

You should avoid using object property shorthand in the following situations:

- **When property names and variable names differ**: If the key and variable name are not the same, shorthand isn't applicable, and full key-value syntax is required for clarity.

- **When clarity is more important than brevity**: In complex objects or configuration files, explicitly naming keys and values can improve readability and reduce confusion.

- **In dynamic property assignment**: If you're using computed property names or dynamically constructing object keys, the shorthand does not apply and full syntax is often clearer.

#### Example of when not to use shorthand:

```javascript
const username = "alice";

// ❌ Not using shorthand (names differ)
const user = {
  name: username // Better for readability
};
```