## 1. What is a Symbol in JavaScript?

- A **Symbol** is a unique and immutable primitive value used as an identifier for object properties.
- Symbols help avoid property name collisions, especially when adding properties to objects from different sources or libraries.
- Each Symbol is guaranteed to be unique, even if two Symbols have the same description.

## 2. How do you create a new symbol? Provide syntax.

```js
const mySymbol = Symbol('description');
```
- The optional string `'description'` is used for debugging purposes and does not affect the uniqueness of the Symbol.
## 3. Are symbols primitive or reference types in JavaScript?

- Symbols are **primitive** data types.
- They are immutable and unique values.
- Unlike objects, symbols are not reference types.
## 4. Are two symbols with the same description equal? Why or why not?

- No, two symbols with the same description are **not equal**.
- Each symbol is unique and distinct, regardless of its description.
- The description is only used for debugging and does not affect identity.

## 5. What is the use of the optional description passed when creating a symbol?

- The description is a **human-readable label** for the symbol.
- It helps during debugging or logging to identify the symbol.
- It does **not** affect the uniqueness or behavior of the symbol.
