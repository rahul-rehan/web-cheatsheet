## 1, What is the difference between a normal object and a Proxy object?

- A **normal object** directly stores and manages its properties and behaviors.
- A **Proxy object** wraps a target object and intercepts fundamental operations (like property access, assignment, enumeration) through handler functions called *traps*. This allows customizing or extending the default behavior of the target object without modifying it.

## 2. How does the use of Reflect ensure consistent trap behavior?

- The `Reflect` API provides methods that perform the default behavior of object operations.
- Inside Proxy traps, using `Reflect` methods lets you delegate the operation back to the original target with consistent semantics.
- This prevents unexpected behavior and ensures the traps behave in line with JavaScript's default object model, improving maintainability and correctness.

## 3. Can you proxy arrays or functions? Provide an example.

Yes, you can proxy arrays and functions.

**Example: Proxying an array**

```js
const arr = [1, 2, 3];

const proxyArr = new Proxy(arr, {
  get(target, prop) {
    console.log(`Accessing element ${prop}`);
    return Reflect.get(target, prop);
  }
});

console.log(proxyArr[1]); // Logs: Accessing element 1 \n 2
```
**Example: Proxying a function**

```js
function greet(name) {
  return `Hello, ${name}!`;
}

const proxyFunc = new Proxy(greet, {
  apply(target, thisArg, args) {
    console.log(`Calling function with args: ${args}`);
    return Reflect.apply(target, thisArg, args);
  }
});

console.log(proxyFunc('Alice')); // Logs: Calling function with args: Alice \n Hello, Alice!
```
## 4. What happens if you don’t use Reflect inside a trap handler?

- If you don’t use `Reflect` inside a trap, you must manually implement the default behavior.
- Failing to do so can lead to inconsistent or incorrect behavior because the trap might not fully replicate the target’s original operation.
- It increases complexity and the risk of bugs since traps must handle all edge cases explicitly.
- Using `Reflect` ensures the trap delegates to the standard behavior, making the Proxy reliable and predictable.

## 5. How can Proxies affect performance and memory?

- Proxies introduce an additional layer of indirection, which can slow down property access and other operations compared to direct access.
- Heavy use of Proxies may increase CPU usage due to trap function calls on every intercepted operation.
- They can also increase memory consumption because Proxy objects keep references to both the target and the handler.
- Thus, while powerful, Proxies should be used judiciously in performance-critical code.

## Real-world Use Cases
## 1. How can Proxies be used for API request interception or rate limiting?

- Proxies can wrap API request objects or functions to intercept calls.
- By using the `apply` or `get` traps, you can monitor, modify, or block requests dynamically.
- This enables implementing rate limiting by tracking request counts and timing inside the trap.
- You can also add logging, caching, or request throttling transparently via Proxy handlers.

## 2. How can Proxies help implement reactive data systems (e.g., Vue.js reactivity)?

- Proxies can intercept property access (`get`) and updates (`set`) on reactive state objects.
- When a property is read or changed, the Proxy trap can trigger dependency tracking or notify observers.
- This allows frameworks like Vue.js to detect changes and automatically update the UI.
- Proxies provide a clean, native way to implement reactivity without intrusive getters/setters.

## 3. Can Proxies be used to simulate private properties or enforce security rules?

- Yes, Proxies can restrict access to certain properties by intercepting and controlling `get`, `set`, or `deleteProperty` operations.
- They can hide or block access to "private" fields by filtering property keys or throwing errors on unauthorized access.
- Proxies can enforce security policies, e.g., making objects read-only, preventing deletion, or validating values before assignment.
- While not true private properties, Proxies provide a flexible layer for encapsulation and access control.
## 4. Provide an example of combining Proxy and Reflect for custom behavior

You can combine `Proxy` and `Reflect` to create custom behavior while maintaining default object operations. Here's an example that logs property access but still behaves like a normal object:

```javascript
const user = {
  name: "Alice",
  age: 30
};

const handler = {
  get(target, prop, receiver) {
    console.log(`Accessed property: ${prop}`);
    return Reflect.get(target, prop, receiver);
  },
  set(target, prop, value, receiver) {
    console.log(`Setting ${prop} to ${value}`);
    return Reflect.set(target, prop, value, receiver);
  }
};

const proxyUser = new Proxy(user, handler);

console.log(proxyUser.name); // Logs "Accessed property: name", then "Alice"
proxyUser.age = 31;          // Logs "Setting age to 31"
```
## 5. When should you avoid using Proxy in an application?

Using `Proxy` can be powerful, but there are situations where it is better to avoid them:

- **Performance Overhead**: Proxies introduce additional function calls and logic that may impact performance, especially in performance-critical applications or tight loops.

- **Limited Browser/Environment Support**: Although widely supported in modern environments, older browsers (like Internet Explorer) do not support Proxies at all.

- **Tooling Limitations**: Some developer tools, serializers (e.g., `JSON.stringify()`), and libraries may not work correctly or as expected with Proxy-wrapped objects.

- **Debugging Difficulty**: Proxies can obscure object behavior, making debugging harder if developers are not aware a Proxy is involved.

- **Memory Leaks**: Improper use of Proxies, especially when used globally or with long-lived references, can potentially cause memory leaks.

- **Complexity**: If used without clear purpose, Proxies can make code harder to read and maintain.

**Recommendation**: Use Proxy only when you need dynamic behavior that cannot be achieved easily with standard patterns. For most use cases, simpler alternatives (like classes, functions, or observers) are preferable.
