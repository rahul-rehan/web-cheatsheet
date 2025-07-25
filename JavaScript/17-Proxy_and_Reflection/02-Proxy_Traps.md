## 1. What does the get trap do in a Proxy?

The **get** trap intercepts property access on the proxy object. It is called whenever a property is read, allowing you to customize or control what value is returned.

**Example:**

```js
const target = { message: "Hello" };
const proxy = new Proxy(target, {
  get(obj, prop) {
    if (prop === "message") {
      return "Intercepted: " + obj[prop];
    }
    return obj[prop];
  }
});

console.log(proxy.message); // Output: Intercepted: Hello
```
## 2. What does the set trap do in a Proxy?

The **set** trap intercepts property assignments on the proxy object. It allows you to control, validate, or modify the values being assigned before they are set on the target object.

**Example:**

```js
const target = {};
const proxy = new Proxy(target, {
  set(obj, prop, value) {
    if (typeof value === "number") {
      obj[prop] = value;
      return true; // Indicate success
    } else {
      throw new TypeError("Only numbers allowed");
    }
  }
});

proxy.age = 25;    // Works fine
proxy.name = "Bob"; // Throws TypeError
```
## 3. How does the `has` trap work? Provide an example.

The **`has`** trap intercepts the `in` operator when checking if a property exists in the proxy object. It allows you to customize or control the behavior of property existence checks.

**Example:**

```js
const target = { name: "Alice", age: 30 };
const proxy = new Proxy(target, {
  has(obj, prop) {
    if (prop === "secret") {
      return false; // Hide the "secret" property even if it exists
    }
    return prop in obj; // Default behavior for other properties
  }
});

console.log("name" in proxy);   // true
console.log("age" in proxy);    // true
console.log("secret" in proxy); // false (even if target.secret exists)
```
## 4. What is the purpose of the `deleteProperty` trap?

The **`deleteProperty`** trap intercepts attempts to delete properties from the proxy object (using the `delete` operator). It allows custom behavior or control over property deletion.

**Example use cases:**
- Prevent deletion of certain properties.
- Log or validate property deletions.
- Modify the delete operation behavior.

## 5. How does the `ownKeys` trap work?

The **`ownKeys`** trap intercepts operations that list the object's own property keys, such as:
- `Object.getOwnPropertyNames()`
- `Object.getOwnPropertySymbols()`
- `Object.keys()`
- `Reflect.ownKeys()`

It returns an array of property keys (strings and/or symbols) that the proxy should report as its own properties.

This trap allows customization of which properties are visible during key enumeration.

**Example:**

```js
const target = { a: 1, b: 2, c: 3 };
const proxy = new Proxy(target, {
  ownKeys(obj) {
    return ['a', 'c']; // Hide property 'b' from enumeration
  }
});

console.log(Object.keys(proxy)); // ['a', 'c']
```
## 6. What does the `apply` trap handle in a Proxy?

The **`apply`** trap intercepts function calls made on the proxy. It allows you to customize the behavior when the proxy is invoked as a function.

- It is only valid if the proxy wraps a function object.
- The trap receives three arguments: the target function, the `this` context, and the arguments list.

**Use cases:**
- Logging or modifying function calls.
- Wrapping or decorating functions.
- Controlling or validating arguments.

## 7. When is the `construct` trap used?

The **`construct`** trap intercepts calls to the proxy using the `new` operator, i.e., when the proxy is used as a constructor.

- It allows you to customize or override the behavior of object instantiation.
- The trap receives two arguments: the target constructor function and an array of arguments passed to `new`.

**Use cases:**
- Creating custom instances.
- Logging or modifying constructor behavior.
- Proxying class instantiation.