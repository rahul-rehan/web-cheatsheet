## 1. What are the two main phases of an execution context?

An execution context goes through **two main phases**:
1. **Creation Phase** (also called the **Memory Creation Phase**)
2. **Execution Phase**


## 2. What happens during the creation phase of an execution context?

During the **creation phase**, JavaScript performs the following tasks:
- **Creation of the Variable Object (VO):** It sets up memory space for variables, functions, and arguments.
- **Hoisting:**  
  - Function declarations are fully hoisted (available in memory with their definitions).  
  - Variables are hoisted but initialized with `undefined`.
- **Scope Chain Setup:** Establishes the scope chain to maintain access to outer environments.
- **Determine the value of `this`:** The context for `this` is set.

## 3. What happens during the execution phase of an execution context?

During the **execution phase**, JavaScript:
- Executes the code line-by-line.
- Assigns values to variables and evaluates expressions.
- Invokes functions and executes their code (creating new execution contexts as needed).
- Updates variable values as the program runs.

---

**In short:**  
- The **creation phase** prepares the environment (allocates memory, hoists functions and variables).  
- The **execution phase** actually runs the code and updates values.
## 4. What is the role of the variable environment in the creation phase?

The **variable environment** is a component of the execution context created during the **creation phase**. Its role is to:
- Store all variable and function declarations within that context.
- Manage the memory allocation for variables and functions before the code runs.
- Support **hoisting** by initializing variables with `undefined` and fully registering function declarations.
- Keep track of the current variables and their values as the program executes.

Essentially, the variable environment acts as the place where variables and functions live inside an execution context.

## 5. What is the lexical environment, and how is it different from variable environment?

- **Lexical Environment**:  
  A **lexical environment** is a data structure that holds the association between variable names and their values **along with a reference to its outer (parent) lexical environment**. It reflects the **static (lexical) scope** of the code — meaning where variables and functions are physically written in the source code.

- **Difference from Variable Environment**:  
  While the **variable environment** specifically tracks variables and function declarations during the creation phase of an execution context, the **lexical environment** is a broader concept that also includes the **reference to the outer environment (scope chain)**.  
  In many modern JavaScript engines, the variable environment is implemented as part of the lexical environment, but conceptually:  
  - The **variable environment** focuses on variable storage inside the current context.  
  - The **lexical environment** manages both variable storage **and** the scope chain for resolving identifiers.

---

**Summary:**

| Aspect              | Variable Environment                          | Lexical Environment                           |
|---------------------|----------------------------------------------|-----------------------------------------------|
| Purpose             | Stores variables and functions in current context during creation phase | Stores variables/functions and reference to outer environment (scope chain) |
| Includes            | Variables, functions, arguments               | Variables, functions, arguments, and outer lexical environment reference |
| When used           | Mainly during creation phase of execution context | Throughout code execution for scope resolution |
| Relation            | Often considered part or a component of lexical environment | Broader concept that includes variable environment plus scope chain link |
