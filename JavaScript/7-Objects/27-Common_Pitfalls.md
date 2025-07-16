## 1. Why might relying on `window` or `global` lead to compatibility issues?

- `window` exists only in browser environments.
- `global` exists only in Node.js.
- Using either directly can cause errors or undefined behavior when code runs in environments where those objects do not exist.
- This leads to compatibility issues across different JavaScript environments (browsers, Node.js, Web Workers, etc.).

## 2. Can `globalThis` be overwritten or reassigned?

- Technically, the `globalThis` reference **can** be reassigned in non-strict mode, but it is **strongly discouraged**.
- Overwriting `globalThis` can break assumptions made by libraries and the runtime, causing unpredictable behavior.
- Modern JavaScript environments typically make `globalThis` a read-only reference or discourage reassignment.

## 3. Is it recommended to pollute the global scope using `globalThis`? Why or why not?

- **No, it is not recommended** to pollute the global scope, whether via `globalThis` or other globals.
- Polluting the global scope can lead to naming collisions, bugs, and maintenance challenges.
- It is better to encapsulate variables and functions within modules, closures, or namespaces to avoid unintended side effects and improve code modularity and testability.
## 4. How can using `globalThis` aid in library or framework development?

- Provides a **unified, environment-agnostic** way to access the global object across browsers, Node.js, and other JavaScript environments.
- Helps libraries/frameworks avoid environment-specific checks like `typeof window !== 'undefined'` or `typeof global !== 'undefined'`.
- Simplifies writing **cross-platform compatible** code by using a single global reference.
- Reduces bugs and increases maintainability when the same codebase runs in multiple environments.


## 5. What precautions should you take when working with global variables via `globalThis`?

- **Avoid polluting the global namespace**: Minimize adding properties or functions to `globalThis` to prevent conflicts.
- **Use unique names or namespaces** to reduce risk of overwriting existing globals.
- **Check for existence before creating new globals** to avoid overwriting or duplicating.
- Be aware that global variables persist for the lifetime of the environment, potentially causing memory leaks.
- Prefer modular or scoped design patterns instead of relying on globals whenever possible.
