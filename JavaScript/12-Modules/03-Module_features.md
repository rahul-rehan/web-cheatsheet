## 1. Are JavaScript modules singleton? Explain.

Yes, JavaScript modules are singletons. When a module is imported multiple times across different files, it is **only instantiated once**. The module's code is executed a single time, and its exports are cached. All importers receive the same shared instance, ensuring consistent state throughout the application.

## 2. Are imports hoisted in ES6 modules?

Yes, ES6 module imports are **hoisted**. This means that import statements are processed before any code in the module runs, allowing imported bindings to be available throughout the entire module, even if they are used before the actual import statement in the code.

## 3. What is the execution order of JavaScript modules?

1. **Dependency Resolution:** The module loader first resolves all dependencies recursively.
2. **Module Instantiation:** Modules are instantiated once dependencies are known.
3. **Module Evaluation:** Modules are executed in dependency order — a module's dependencies are executed before the module itself.
4. **Exports Are Cached:** After execution, exports are cached for reuse by other modules.

This ensures that modules execute only once and in the correct order based on their import relationships.
## 4. Can you use conditional statements to import modules? Why or why not?

No, you **cannot use conditional statements with static `import` syntax** because imports are hoisted and must be declared at the top level of the module. This static nature allows the JavaScript engine to analyze and optimize dependencies before execution.

However, **dynamic `import()`** can be used conditionally since it returns a Promise and can be called anywhere in the code:

```js
if (condition) {
  import('./module.js').then(module => {
    // use the module
  });
}
```
## 5. What happens if a module has a syntax error?

If a module contains a syntax error, the module **fails to load**, and a **syntax error is thrown** immediately. This error prevents the module and any dependent modules from executing, typically resulting in a runtime failure or an unhandled exception.

## 6. How does JavaScript ensure module encapsulation?

JavaScript modules have their **own scope** separate from the global scope. Variables, functions, and classes declared inside a module are **not accessible outside** unless explicitly exported.

This encapsulation is ensured by:

- Modules being evaluated in their own scope.
- Only explicitly exported bindings are accessible to importing modules.
- Imported bindings are read-only views of the exported values, preventing external modification of the module's internal state.
