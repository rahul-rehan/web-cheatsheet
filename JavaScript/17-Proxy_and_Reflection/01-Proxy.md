## 1. What is a Proxy in JavaScript?

A **Proxy** is an object that wraps another object (called the *target*) and intercepts operations performed on it, such as property access, assignment, enumeration, function invocation, etc. It allows customizing or redefining fundamental behaviors of the target object.

## 2. What are the main use cases for using a Proxy?

- **Validation:** Intercept and validate property assignments.
- **Logging or debugging:** Track operations on objects like property reads or writes.
- **Default values:** Provide default responses when accessing missing properties.
- **Revocable references:** Create objects that can be disabled or revoked.
- **Access control:** Restrict or modify access to certain properties.
- **Reactive programming:** Automatically track dependencies and trigger reactions on property changes (used in frameworks like Vue.js).

## 3. How do you create a new Proxy object? Provide basic syntax.

```js
const proxy = new Proxy(target, handler);
```
- **target:** The original object to wrap.

- **handler:** An object defining traps (methods) to intercept operations on the target.
#### Example:

```js
const target = {};
const handler = {
  get: function(obj, prop) {
    return prop in obj ? obj[prop] : 'Property not found';
  }
};

const proxy = new Proxy(target, handler);

console.log(proxy.foo); // Output: Property not found
```
## 4. What are "traps" in the context of a Proxy?

**Traps** are special methods defined in the handler object of a Proxy that intercept and customize operations performed on the target object. Each trap corresponds to a specific operation, such as:

- `get` — intercepts property access
- `set` — intercepts property assignment
- `has` — intercepts the `in` operator
- `deleteProperty` — intercepts property deletion
- `apply` — intercepts function calls (when the target is a function)
- `construct` — intercepts the `new` operator

By defining traps, you control how the proxy responds to these operations.

## 5. What are the two required parameters to create a Proxy?

To create a Proxy, you must provide:

1. **target:** The original object (or function) to be wrapped by the Proxy.
2. **handler:** An object containing traps that define the custom behavior for operations on the target.

**Syntax:**

```js
const proxy = new Proxy(target, handler);
```