## 1. How can Symbol be used as an object property key?

- You can use a symbol as a key by defining it in square brackets when creating or accessing object properties.
- Example:
  ```js
  const sym = Symbol('uniqueKey');
  const obj = {
    [sym]: 'value'
  };
  ```
## 2. What are the benefits of using symbols as property keys?

- **Uniqueness:** Symbols ensure property keys are unique, preventing naming collisions.
- **Non-enumerability:** Properties keyed by symbols do not appear in typical enumeration methods like `for...in` loops or `Object.keys()`.
- **Encapsulation:** Symbols can be used to create private or hidden object properties that are not easily accessible.

## 3. How can you access a property defined with a symbol key?

- You access the property by using the symbol as the key inside square brackets:
  ```js
  const sym = Symbol('key');
  const obj = { [sym]: 'value' };
  console.log(obj[sym]); // Outputs: 'value'
  ```
- Symbol properties cannot be accessed using dot notation or string keys.
## 4. Are symbol-keyed properties enumerable in `for...in` loops or `Object.keys()`?

No, symbol-keyed properties are **not enumerable** in `for...in` loops or returned by `Object.keys()`. They are hidden from typical property enumerations.

## 5. How can you list all symbol properties of an object?

You can list all symbol properties using the `Object.getOwnPropertySymbols()` method:

```js
const sym1 = Symbol('foo');
const sym2 = Symbol('bar');

const obj = {
  [sym1]: 123,
  [sym2]: 456,
  normalProp: 'abc'
};

const symbols = Object.getOwnPropertySymbols(obj);
console.log(symbols); // [Symbol(foo), Symbol(bar)]
```
## 6. Provide an example where using a symbol avoids name collision in object properties.

```js
const symId = Symbol('id');

const user = {
  name: 'Alice',
  [symId]: 12345
};

// Later in the code, another property named 'id' is added without collision:
user.id = 'user_1';

console.log(user.name);      // Alice
console.log(user.id);        // 'user_1'
console.log(user[symId]);    // 12345 (unique symbol key avoids collision)
```
In this example, the symbol-keyed property `[symId]` avoids collision with the string-keyed property `'id'`.