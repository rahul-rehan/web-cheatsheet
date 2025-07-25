## 1. How does Symbol differ from String or Number as object keys?

Symbols differ from strings and numbers when used as object keys in the following ways:

- **Uniqueness**: Every symbol is unique, even if they have the same description. This avoids property name collisions.
- **Non-enumerable by default**: Symbol-keyed properties do not show up in `for...in`, `Object.keys()`, or `JSON.stringify()`.
- **Hidden/Internal properties**: Symbols are often used to define "hidden" or internal properties that won't accidentally clash with other keys.

## 2. Can you stringify an object with symbol keys using JSON.stringify()?

No, `JSON.stringify()` ignores properties whose keys are Symbols. These properties are omitted from the resulting JSON string.

**Example:**
```js
const sym = Symbol("id");
const obj = { [sym]: 123, name: "John" };

console.log(JSON.stringify(obj)); 
// Output: {"name":"John"} — symbol key is ignored
```
## 3. How do symbols behave when spread with the spread operator (...)?

When using the spread operator (`...`) on objects, **symbol-keyed properties are not included** by default. The spread operator only copies **own enumerable string-keyed properties**.

#### Example:
```js
const sym = Symbol('hidden');
const obj = {
  [sym]: 'secret value',
  visible: 'public value'
};

const copy = { ...obj };

console.log(copy); // Output: { visible: 'public value' }
console.log(copy[sym]); // Output: undefined
```
#### Including symbol properties manually:
To include symbol-keyed properties, use Object.`getOwnPropertySymbols() or Reflect.ownKeys()`:

```js
const clone = {
  ...obj,
  ...Object.fromEntries(
    Object.getOwnPropertySymbols(obj).map(sym => [sym, obj[sym]])
  )
};

console.log(clone[sym]); // Output: 'secret value'
```
## 4. Can you clone symbol properties when using Object.assign()?

Yes, `Object.assign()` **copies symbol-keyed properties** along with string-keyed enumerable own properties from the source object to the target object.

#### Example:
```js
const sym = Symbol('id');
const source = {
  [sym]: 123,
  name: 'Alice'
};

const target = Object.assign({}, source);
console.log(target[sym]); // Output: 123
console.log(target.name); // Output: 'Alice'
```
## 5. Can symbols be used in computed property names?

Yes, symbols **can be used as computed property names** in object literals by placing the symbol inside square brackets (`[]`). This allows you to create properties keyed by symbols.

#### Example:
```js
const sym = Symbol('example');

const obj = {
  [sym]: 'This is a symbol-keyed property'
};

console.log(obj[sym]); // Output: 'This is a symbol-keyed property'
```
Using symbols as computed property names helps avoid name collisions and keeps properties hidden from standard enumeration methods like `for...in or Object.keys()`.

## Advanced and Best Practices
## 1. When should you use a Symbol over a String for a property key?

You should use a `Symbol` instead of a string for a property key when:
- You want to create **unique, non-colliding property keys**, especially in shared or third-party objects.
- You want to **hide internal implementation details** of objects.
- You need to define **meta-level behaviors**, such as customizing iteration with `Symbol.iterator`.

## 2. How does using Symbol improve code encapsulation or private-like behavior?

Symbols provide a way to add **semi-private** properties to objects:
- Properties keyed with symbols are **not accessible via normal iteration** (`for...in`, `Object.keys()`), reducing the chance of accidental access or modification.
- Symbols help **avoid naming conflicts**, especially when multiple libraries or components augment the same object.
- Although not truly private, symbol properties are **harder to access without direct reference to the Symbol**.

## 3. What are the limitations of using symbols in JavaScript?

- **Not truly private**: While symbols reduce visibility, they don’t prevent access — tools like `Object.getOwnPropertySymbols()` can still retrieve them.
- **Not included in JSON**: `JSON.stringify()` omits symbol-keyed properties.
- **Limited introspection**: Debugging symbol properties can be harder due to their opaque nature.
- **May reduce readability**: Overusing symbols can make code harder to understand, especially for newcomers.
## 4. Can you use symbols to implement private fields in objects?

Yes, symbols can be used to simulate private fields in objects. Since symbol-keyed properties are not accessible through standard property enumeration (like `for...in`, `Object.keys()`, or `JSON.stringify()`), they provide a layer of obscurity. While not truly private, they make accidental access or collisions less likely.

#### Example:
```js
const _secret = Symbol('secret');

const obj = {
  [_secret]: 'hidden value',
  reveal() {
    return this[_secret];
  }
};

console.log(obj.reveal()); // 'hidden value'
console.log(obj._secret);  // undefined
```
## 5. How can symbols support metaprogramming patterns in JavaScript?

Symbols enable metaprogramming by allowing developers to define or override the default behavior of built-in operations through **well-known symbols**. These symbols act as hooks into JavaScript's internal mechanisms and can be used to customize object interactions in powerful ways.

#### Common use cases of well-known symbols in metaprogramming:

- **`Symbol.iterator`**: Makes objects iterable with `for...of` loops.
- **`Symbol.toPrimitive`**: Customizes how objects are converted to primitives.
- **`Symbol.toStringTag`**: Alters the tag returned by `Object.prototype.toString`.
- **`Symbol.hasInstance`**: Customizes behavior of the `instanceof` operator.
- **`Symbol.isConcatSpreadable`**: Controls spread behavior in array concatenation.

#### Example – Custom Iteration using `Symbol.iterator`:
```js
const myIterable = {
  *[Symbol.iterator]() {
    yield 'a';
    yield 'b';
    yield 'c';
  }
};

for (const value of myIterable) {
  console.log(value); // 'a', 'b', 'c'
}
```
Using these symbols allows developers to create highly flexible, expressive APIs and build advanced abstractions that interact deeply with the JavaScript runtime.