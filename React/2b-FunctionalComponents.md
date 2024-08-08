# Function Component

### 1. **What are functional components in React?**

Functional components are a simpler way to create components in React. They are defined as JavaScript functions that accept props as arguments and return React elements. Unlike class-based components, functional components do not have their own state or lifecycle methods by default, but they can use Hooks to manage state and side effects.

**Example:**

```javascript
import React from 'react';

const MyFunctionalComponent = (props) => {
  return <h1>Hello, {props.name}!</h1>;
};

export default MyFunctionalComponent;
```

### 2. **How do functional components differ from class-based components?**

- **Syntax**:
  - **Functional Components**: Defined using functions. Simpler and more concise.
    ```javascript
    const MyFunctionalComponent = (props) => {
      return <h1>Hello, {props.name}!</h1>;
    };
    ```

  - **Class-based Components**: Defined using ES6 class syntax. More verbose and includes lifecycle methods.
    ```javascript
    import React, { Component } from 'react';

    class MyClassComponent extends Component {
      render() {
        return <h1>Hello, {this.props.name}!</h1>;
      }
    }
    ```

- **State and Lifecycle Methods**:
  - **Functional Components**: Initially stateless, but can use Hooks (e.g., `useState`, `useEffect`) for state and side effects.
    ```javascript
    import React, { useState } from 'react';

    const Counter = () => {
      const [count, setCount] = useState(0);

      return (
        <div>
          <p>{count}</p>
          <button onClick={() => setCount(count + 1)}>Increment</button>
        </div>
      );
    };
    ```

  - **Class-based Components**: Use `this.state` for state and lifecycle methods like `componentDidMount` for side effects.
    ```javascript
    import React, { Component } from 'react';

    class Counter extends Component {
      constructor(props) {
        super(props);
        this.state = { count: 0 };
      }

      increment = () => {
        this.setState({ count: this.state.count + 1 });
      }

      render() {
        return (
          <div>
            <p>{this.state.count}</p>
            <button onClick={this.increment}>Increment</button>
          </div>
        );
      }
    }
    ```

### 3. **What are the benefits of using functional components?**

- **Simplicity**: Functional components are less verbose and easier to understand, making them ideal for simpler components.
- **Hooks**: With the introduction of Hooks, functional components can manage state and side effects, which was previously a limitation.
- **Performance**: Functional components can be more performant since they don’t have the overhead of class instances.
- **Less Boilerplate**: No need for `this` binding or class methods, which reduces boilerplate code.

**Example with Hooks:**

```javascript
import React, { useState, useEffect } from 'react';

const Example = () => {
  const [count, setCount] = useState(0);

  useEffect(() => {
    document.title = `You clicked ${count} times`;
  }, [count]);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>Click me</button>
    </div>
  );
};

export default Example;
```

### 4. **How do you pass data to a functional component?**

Data is passed to functional components via props, which are arguments to the function.

**Example:**

```javascript
import React from 'react';

const Greeting = (props) => {
  return <h1>Hello, {props.name}!</h1>;
};

const App = () => {
  return <Greeting name="Alice" />;
};

export default App;
```

In this example, the `name` prop is passed to the `Greeting` component.

### 5. **Can you explain how props work in functional components?**

Props are inputs to a functional component that allow you to pass data and event handlers from parent components. They are accessed directly within the functional component as function arguments.

**Example:**

```javascript
import React from 'react';

const UserProfile = ({ name, age, onClick }) => {
  return (
    <div>
      <h2>{name}</h2>
      <p>Age: {age}</p>
      <button onClick={onClick}>Click Me</button>
    </div>
  );
};

const App = () => {
  const handleClick = () => {
    alert('Button clicked');
  };

  return (
    <UserProfile name="Bob" age={30} onClick={handleClick} />
  );
};

export default App;
```

In this example, `name`, `age`, and `onClick` are props passed to the `UserProfile` component.

### 6. **How would you handle default props in a functional component?**

Default props can be specified using the `defaultProps` property of the functional component. This allows you to define default values for props if they are not provided.

**Example:**

```javascript
import React from 'react';

const Greeting = ({ name }) => {
  return <h1>Hello, {name}!</h1>;
};

Greeting.defaultProps = {
  name: 'Guest'
};

const App = () => {
  return <Greeting />;
};

export default App;
```

In this example, if the `name` prop is not provided, it defaults to `'Guest'`.

### 7. **How does JSX work within functional components?**

JSX (JavaScript XML) is a syntax extension that allows you to write HTML-like code within JavaScript. In functional components, JSX is used to define the component's UI structure. React compiles JSX into JavaScript objects that represent the UI elements.

**Example:**

```javascript
import React from 'react';

const MyComponent = () => {
  return (
    <div>
      <h1>Hello, World!</h1>
      <p>This is a functional component using JSX.</p>
    </div>
  );
};

export default MyComponent;
```

In this example, JSX is used to describe the structure of the UI. React transforms the JSX into `React.createElement` calls, which create JavaScript objects representing the DOM elements.

### 8. **What is the purpose of the return statement in a functional component?**

The `return` statement in a functional component specifies the UI that the component should render. It returns JSX or `null` (if nothing should be rendered).

**Example:**

```javascript
import React from 'react';

const MyComponent = () => {
  return (
    <div>
      <h1>Welcome to My Component</h1>
    </div>
  );
};

export default MyComponent;
```

In this example, the `return` statement specifies that the component should render a `div` containing an `h1` element.

### 9. **How can you conditionally render elements in a functional component?**

Conditional rendering in functional components can be achieved using JavaScript conditional operators (like `if`, ternary operators) or logical operators.

**Examples:**

- **Using Ternary Operator:**

  ```javascript
  import React from 'react';

  const MyComponent = ({ isLoggedIn }) => {
    return (
      <div>
        {isLoggedIn ? <p>Welcome back!</p> : <p>Please log in.</p>}
      </div>
    );
  };

  export default MyComponent;
  ```

- **Using Logical AND Operator:**

  ```javascript
  import React from 'react';

  const MyComponent = ({ showMessage }) => {
    return (
      <div>
        {showMessage && <p>This message is shown based on a condition.</p>}
      </div>
    );
  };

  export default MyComponent;
  ```

### 10. **What are React Hooks and how do they relate to functional components?**

React Hooks are functions that let you use state and other React features in functional components. They allow you to manage state, side effects, context, and more without needing class-based components.

**Common Hooks Include:**
- **`useState`**: Manages state in functional components.
- **`useEffect`**: Handles side effects (e.g., data fetching, subscriptions).
- **`useContext`**: Accesses context values.
- **`useReducer`**: Manages complex state logic.

**Example of `useState` and `useEffect`:**

```javascript
import React, { useState, useEffect } from 'react';

const ExampleComponent = () => {
  const [count, setCount] = useState(0);

  useEffect(() => {
    document.title = `Count: ${count}`;
  }, [count]);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
};

export default ExampleComponent;
```

### 11. **Explain the difference between `useState` and `useEffect` hooks.**

- **`useState`**:
  - **Purpose**: Manages local state in a functional component.
  - **Usage**: Provides a state variable and a function to update that state.
  
  **Example:**
  ```javascript
  import React, { useState } from 'react';

  const Counter = () => {
    const [count, setCount] = useState(0);

    return (
      <div>
        <p>Count: {count}</p>
        <button onClick={() => setCount(count + 1)}>Increment</button>
      </div>
    );
  };

  export default Counter;
  ```

- **`useEffect`**:
  - **Purpose**: Handles side effects (e.g., data fetching, subscriptions) in a functional component.
  - **Usage**: Runs after every render by default or based on dependencies specified in the second argument.
  
  **Example:**
  ```javascript
  import React, { useState, useEffect } from 'react';

  const DataFetcher = () => {
    const [data, setData] = useState(null);

    useEffect(() => {
      fetch('https://api.example.com/data')
        .then(response => response.json())
        .then(data => setData(data));
    }, []); // Empty dependency array means it runs once after the initial render

    return (
      <div>
        {data ? <pre>{JSON.stringify(data, null, 2)}</pre> : <p>Loading...</p>}
      </div>
    );
  };

  export default DataFetcher;
  ```

### 12. **Can you provide an example of using a custom hook in a functional component?**

Custom hooks allow you to extract reusable logic from components into functions. They follow the naming convention `useCustomHook` and can use other hooks internally.

**Example of a Custom Hook:**

1. **Define the Custom Hook:**

  ```javascript
  import { useState, useEffect } from 'react';

  const useWindowWidth = () => {
    const [windowWidth, setWindowWidth] = useState(window.innerWidth);

    useEffect(() => {
      const handleResize = () => setWindowWidth(window.innerWidth);

      window.addEventListener('resize', handleResize);

      // Clean up the event listener
      return () => window.removeEventListener('resize', handleResize);
    }, []);

    return windowWidth;
  };

  export default useWindowWidth;
  ```

2. **Use the Custom Hook in a Component:**

  ```javascript
  import React from 'react';
  import useWindowWidth from './useWindowWidth';

  const WindowWidthDisplay = () => {
    const windowWidth = useWindowWidth();

    return (
      <div>
        <p>Current window width: {windowWidth}px</p>
      </div>
    );
  };

  export default WindowWidthDisplay;
  ```

In this example, `useWindowWidth` is a custom hook that provides the current window width and updates it on window resize. The `WindowWidthDisplay` component uses this hook to display the width.

### 13. **How can you handle component lifecycle methods (e.g., `componentDidMount`) using hooks?**

In functional components, lifecycle methods are managed using the `useEffect` hook. `useEffect` allows you to perform side effects in your component. It can mimic lifecycle methods like `componentDidMount`, `componentDidUpdate`, and `componentWillUnmount`.

**Example of `useEffect` mimicking `componentDidMount`:**

```javascript
import React, { useEffect, useState } from 'react';

const MyComponent = () => {
  const [data, setData] = useState(null);

  useEffect(() => {
    // This code runs once after the component mounts, similar to componentDidMount
    fetch('https://api.example.com/data')
      .then(response => response.json())
      .then(data => setData(data))
      .catch(error => console.error('Error fetching data:', error));
  }, []); // Empty dependency array means this effect runs only once

  return (
    <div>
      {data ? <pre>{JSON.stringify(data, null, 2)}</pre> : <p>Loading...</p>}
    </div>
  );
};

export default MyComponent;
```

**Example of `useEffect` mimicking `componentWillUnmount`:**

```javascript
import React, { useEffect, useState } from 'react';

const TimerComponent = () => {
  const [seconds, setSeconds] = useState(0);

  useEffect(() => {
    const timerId = setInterval(() => {
      setSeconds(prevSeconds => prevSeconds + 1);
    }, 1000);

    // Cleanup function runs on unmount, similar to componentWillUnmount
    return () => clearInterval(timerId);
  }, []); // Empty dependency array means this effect runs once on mount

  return <p>Timer: {seconds} seconds</p>;
};

export default TimerComponent;
```

### 14. **How would you optimize performance in a functional component?**

**Performance optimization techniques for functional components include:**

- **Using `React.memo`**: Prevents re-rendering of a component if its props haven't changed.
  
  ```javascript
  import React, { memo } from 'react';

  const MyComponent = ({ value }) => {
    console.log('Rendering:', value);
    return <div>{value}</div>;
  };

  export default memo(MyComponent);
  ```

- **Using `useCallback`**: Memoizes callback functions to prevent re-creation on every render.

  ```javascript
  import React, { useCallback, useState } from 'react';

  const MyComponent = () => {
    const [count, setCount] = useState(0);

    const handleClick = useCallback(() => {
      setCount(count + 1);
    }, [count]);

    return <button onClick={handleClick}>Increment</button>;
  };

  export default MyComponent;
  ```

- **Using `useMemo`**: Memoizes expensive computations.

  ```javascript
  import React, { useMemo, useState } from 'react';

  const ExpensiveComponent = ({ numbers }) => {
    const sum = useMemo(() => {
      console.log('Calculating sum...');
      return numbers.reduce((a, b) => a + b, 0);
    }, [numbers]);

    return <div>Sum: {sum}</div>;
  };

  export default ExpensiveComponent;
  ```

### 15. **Explain how to test functional components effectively.**

Testing functional components can be done using tools like Jest and React Testing Library. React Testing Library encourages testing components as the users would interact with them.

**Example using React Testing Library:**

1. **Installation:**

   ```sh
   npm install --save-dev @testing-library/react @testing-library/jest-dom
   ```

2. **Test File (`MyComponent.test.js`):**

   ```javascript
   import React from 'react';
   import { render, screen, fireEvent } from '@testing-library/react';
   import '@testing-library/jest-dom/extend-expect';
   import MyComponent from './MyComponent';

   test('renders MyComponent with a button click', () => {
     render(<MyComponent />);

     const button = screen.getByText(/Click me/i);
     fireEvent.click(button);

     expect(screen.getByText(/Clicked/i)).toBeInTheDocument();
   });
   ```

   In this example, we render `MyComponent`, simulate a button click, and then check if the expected output is present in the document.

### 16. **Discuss the use of higher-order components (HOCs) with functional components.**

Higher-Order Components (HOCs) are functions that take a component and return a new component with enhanced functionality. They work with both class-based and functional components.

**Example HOC with Functional Component:**

1. **Define HOC:**

   ```javascript
   import React from 'react';

   const withLoading = (WrappedComponent) => {
     return ({ isLoading, ...props }) => {
       if (isLoading) {
         return <p>Loading...</p>;
       }
       return <WrappedComponent {...props} />;
     };
   };

   export default withLoading;
   ```

2. **Use HOC:**

   ```javascript
   import React from 'react';
   import withLoading from './withLoading';

   const DataDisplay = ({ data }) => {
     return <div>Data: {data}</div>;
   };

   export default withLoading(DataDisplay);
   ```

   Here, `withLoading` is a HOC that displays a loading message until data is available.

### 17. **How do functional components fit into the context API in React?**

Functional components can use the Context API to manage and access global state without prop drilling. The `useContext` hook is used to access context values.

**Example:**

1. **Create Context:**

   ```javascript
   import React, { createContext, useState } from 'react';

   export const MyContext = createContext();

   export const MyProvider = ({ children }) => {
     const [value, setValue] = useState('default value');

     return (
       <MyContext.Provider value={{ value, setValue }}>
         {children}
       </MyContext.Provider>
     );
   };
   ```

2. **Consume Context in Functional Component:**

   ```javascript
   import React, { useContext } from 'react';
   import { MyContext } from './MyProvider';

   const DisplayValue = () => {
     const { value } = useContext(MyContext);

     return <div>Context Value: {value}</div>;
   };

   export default DisplayValue;
   ```

   In this example, `DisplayValue` uses the `useContext` hook to access the context value provided by `MyProvider`.

### 18. **Can you compare and contrast functional components with other UI component paradigms?**

**Functional Components vs. Class-based Components:**

- **Simplicity**:
  - **Functional Components**: Simpler and less verbose. Use Hooks for state and lifecycle management.
  - **Class-based Components**: More verbose. Use `this.state` and lifecycle methods.

- **State Management**:
  - **Functional Components**: Use `useState` and `useReducer` Hooks.
  - **Class-based Components**: Use `this.state` and `this.setState`.

- **Lifecycle Management**:
  - **Functional Components**: Use `useEffect` Hook.
  - **Class-based Components**: Use lifecycle methods like `componentDidMount` and `componentWillUnmount`.

**Functional Components vs. UI Components in Other Paradigms (e.g., Vue.js):**

- **Declarative vs. Imperative**:
  - **Functional Components**: React’s approach is declarative, focusing on what the UI should look like.
  - **Vue.js**: Also declarative, but uses templates and directives (e.g., `v-if`, `v-for`) for rendering.

- **Reactivity**:
  - **Functional Components**: React’s state and Hooks manage reactivity.
  - **Vue.js**: Vue’s reactive system is built-in and relies on its `data` and `computed` properties.

- **Component Composition**:
  - **Functional Components**: Use composition and Hooks for reusable logic.
  - **Vue.js**: Uses mixins and composition API for reusable logic.