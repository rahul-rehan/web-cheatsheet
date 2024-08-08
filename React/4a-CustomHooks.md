# Custom Hooks

### 1. What are custom hooks in React, and how do they differ from built-in hooks?

**Custom Hooks:**
- **Definition:** Custom hooks are functions that allow you to extract and reuse stateful logic between components. They are user-defined hooks that leverage built-in hooks (like `useState`, `useEffect`, etc.) to encapsulate complex logic.
- **Difference from Built-in Hooks:** Built-in hooks are provided by React (like `useState`, `useEffect`, `useContext`) and are used to manage state, side effects, and context within functional components. Custom hooks are created by developers to encapsulate and reuse logic across components.

**Example of a Custom Hook:**

```jsx
import { useState, useEffect } from 'react';

// Custom hook to fetch data
const useFetch = (url) => {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    const fetchData = async () => {
      try {
        const response = await fetch(url);
        if (!response.ok) {
          throw new Error('Network response was not ok');
        }
        const result = await response.json();
        setData(result);
      } catch (error) {
        setError(error.message);
      } finally {
        setLoading(false);
      }
    };

    fetchData();
  }, [url]);

  return { data, loading, error };
};

export default useFetch;
```

### 2. Explain the benefits of using custom hooks in React development.

**Benefits of Custom Hooks:**
1. **Code Reusability:** Encapsulate and reuse logic across multiple components, avoiding duplication.
2. **Separation of Concerns:** Separate complex logic into smaller, manageable functions.
3. **Enhanced Readability:** Simplify components by moving complex logic out of them.
4. **Easy Testing:** Custom hooks can be tested in isolation, improving the reliability of your application.

### 3. When would you consider creating a custom hook versus using built-in hooks directly?

**When to Create a Custom Hook:**
- **Reuse Logic:** If you find yourself copying and pasting the same hook logic across different components.
- **Encapsulation:** To encapsulate complex logic or state management that doesn’t fit neatly into a single component.
- **Abstraction:** To abstract away detailed logic that should be managed separately from the UI components.

**Example of Using Built-in Hooks Directly vs. Custom Hook:**

```jsx
// Using built-in hooks directly
const ComponentA = () => {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    const fetchData = async () => {
      try {
        const response = await fetch('https://api.example.com/data');
        if (!response.ok) {
          throw new Error('Network response was not ok');
        }
        const result = await response.json();
        setData(result);
      } catch (error) {
        setError(error.message);
      } finally {
        setLoading(false);
      }
    };

    fetchData();
  }, []);

  if (loading) return <p>Loading...</p>;
  if (error) return <p>Error: {error}</p>;
  return <div>Data: {JSON.stringify(data)}</div>;
};

// Using custom hook
const ComponentB = () => {
  const { data, loading, error } = useFetch('https://api.example.com/data');

  if (loading) return <p>Loading...</p>;
  if (error) return <p>Error: {error}</p>;
  return <div>Data: {JSON.stringify(data)}</div>;
};
```

### 4. What are the two main rules to remember when using hooks in React?

**Two Main Rules for Hooks:**
1. **Call Hooks at the Top Level:** Always call hooks at the top level of a React function. Do not call hooks inside loops, conditions, or nested functions to ensure consistent hook calls on each render.
2. **Call Hooks from React Functions:** Only call hooks from React functional components or other custom hooks. Do not call hooks from regular JavaScript functions.

### 5. Describe some common use cases for custom hooks in React applications.

**Common Use Cases:**
1. **Data Fetching:** Encapsulate data fetching logic to be reused across components.
2. **Form Handling:** Manage form state, validation, and submission logic.
3. **Local Storage Management:** Handle reading from and writing to local storage.
4. **Authentication:** Manage authentication state and logic across components.

**Example of Form Handling Custom Hook:**

```jsx
import { useState } from 'react';

// Custom hook for form management
const useForm = (initialValues) => {
  const [values, setValues] = useState(initialValues);

  const handleChange = (e) => {
    const { name, value } = e.target;
    setValues({
      ...values,
      [name]: value,
    });
  };

  const resetForm = () => setValues(initialValues);

  return [values, handleChange, resetForm];
};

export default useForm;
```

### 6. How can custom hooks help with managing complex state logic?

**Managing Complex State Logic:**
- **Encapsulation:** Custom hooks encapsulate complex state logic and make it reusable across components.
- **Separation of Concerns:** By separating state management logic from UI components, you keep components simpler and more focused on rendering.
- **Custom Logic:** Create custom hooks to handle complex interactions between multiple state variables or side effects.

**Example of Managing Complex State Logic:**

```jsx
import { useState, useEffect } from 'react';

// Custom hook for managing complex state logic
const useComplexState = (initialState) => {
  const [state, setState] = useState(initialState);
  const [status, setStatus] = useState('idle');

  useEffect(() => {
    if (state.isLoading) {
      setStatus('loading');
    } else if (state.hasError) {
      setStatus('error');
    } else {
      setStatus('success');
    }
  }, [state]);

  const updateState = (newState) => {
    setState(prevState => ({
      ...prevState,
      ...newState,
    }));
  };

  return [state, status, updateState];
};

export default useComplexState;
```

In this example, `useComplexState` manages state and status while encapsulating the logic of state updates and status determination. This approach allows for clean and reusable state management across different components.

### 7. Can you explain how to create a custom hook for data fetching using concepts like `useEffect`?

**Custom Hook for Data Fetching:**

Custom hooks for data fetching encapsulate the logic for fetching data, managing loading and error states, and handling asynchronous operations.

**Example:**

```jsx
import { useState, useEffect } from 'react';

// Custom hook for data fetching
const useFetch = (url) => {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    const fetchData = async () => {
      try {
        const response = await fetch(url);
        if (!response.ok) {
          throw new Error('Network response was not ok');
        }
        const result = await response.json();
        setData(result);
      } catch (error) {
        setError(error.message);
      } finally {
        setLoading(false);
      }
    };

    fetchData();
  }, [url]); // Dependency array ensures the hook re-fetches if the URL changes

  return { data, loading, error };
};

export default useFetch;
```

### 8. Provide an example of a custom hook that deals with side effects like subscriptions or timers.

**Custom Hook for Timer:**

A custom hook can manage timers or subscriptions, encapsulating the logic for setting up and cleaning up these side effects.

**Example:**

```jsx
import { useState, useEffect } from 'react';

// Custom hook for managing a timer
const useTimer = (initialTime = 0) => {
  const [time, setTime] = useState(initialTime);

  useEffect(() => {
    const timerId = setInterval(() => {
      setTime(prevTime => prevTime + 1);
    }, 1000);

    // Cleanup function to clear the timer
    return () => clearInterval(timerId);
  }, []);

  return time;
};

export default useTimer;
```

### 9. How do you ensure that your custom hooks are reusable and maintainable?

**Ensuring Reusability and Maintainability:**
1. **Single Responsibility:** Ensure that each hook does one thing well. This makes it easier to reuse and maintain.
2. **Abstract Complex Logic:** Encapsulate complex logic that can be reused across multiple components.
3. **Clear API:** Design custom hooks with a clear and simple API. Use descriptive names and avoid unnecessary parameters.
4. **Document and Comment:** Document what each hook does and how to use it. Include comments to explain non-obvious logic.

**Example:**

```jsx
// Custom hook for form handling
const useForm = (initialValues) => {
  const [values, setValues] = useState(initialValues);

  const handleChange = (e) => {
    const { name, value } = e.target;
    setValues({
      ...values,
      [name]: value,
    });
  };

  return [values, handleChange];
};

export default useForm;
```

### 10. What are some strategies for testing custom hooks effectively?

**Testing Strategies:**
1. **Unit Testing:** Test custom hooks in isolation using libraries like `@testing-library/react-hooks`.
2. **Mock Dependencies:** Mock any external dependencies or API calls to focus on testing the hook’s logic.
3. **Verify State and Effects:** Check that the hook correctly updates state and performs side effects.

**Example:**

```jsx
import { renderHook, act } from '@testing-library/react-hooks';
import useForm from './useForm';

test('should handle form input changes', () => {
  const { result } = renderHook(() => useForm({ name: '' }));

  act(() => {
    result.current[1]({ target: { name: 'name', value: 'John Doe' } });
  });

  expect(result.current[0].name).toBe('John Doe');
});
```

### 11. How can custom hooks be used to improve the organization and readability of your React codebase?

**Improving Organization and Readability:**
1. **Encapsulation of Logic:** Encapsulate complex logic within custom hooks to keep components clean and focused on rendering.
2. **Reuse Across Components:** Reuse hooks across different components to avoid code duplication and enhance maintainability.
3. **Separation of Concerns:** Separate different aspects of component logic (e.g., data fetching, form handling) into separate hooks.

**Example:**

```jsx
import useFetch from './useFetch';
import useForm from './useForm';

const UserProfile = () => {
  const { data, loading, error } = useFetch('/api/user');
  const [formValues, handleInputChange] = useForm({ name: '' });

  if (loading) return <p>Loading...</p>;
  if (error) return <p>Error: {error}</p>;

  return (
    <div>
      <h1>{data.name}</h1>
      <form>
        <input
          type="text"
          name="name"
          value={formValues.name}
          onChange={handleInputChange}
        />
      </form>
    </div>
  );
};

export default UserProfile;
```

### 12. Discuss potential drawbacks or limitations of using custom hooks excessively.

**Drawbacks or Limitations:**
1. **Over-Abstraction:** Excessive use of custom hooks can lead to over-abstraction, making it difficult to understand the flow of data and logic in your application.
2. **Complex Dependencies:** Custom hooks with complex dependencies or side effects can be harder to debug and test.
3. **Performance Considerations:** Improper implementation of custom hooks may lead to performance issues, such as unnecessary re-renders or excessive computations.
4. **Code Sprawl:** Having too many custom hooks can lead to code sprawl, where it becomes challenging to keep track of all the hooks and their interactions.

By carefully designing and using custom hooks, you can avoid these pitfalls and maintain a clean, maintainable codebase.

### 13. Can you differentiate between `useMemo` and `useCallback` hooks, and when would you use each?

**`useMemo`:**
- **Purpose:** Caches the result of a computation and only recomputes it when its dependencies change. It helps in optimizing performance for expensive calculations.
- **Usage:** Use `useMemo` when you have a computation that is expensive to calculate and should only be recalculated when certain dependencies change.

**Example:**

```jsx
import { useMemo } from 'react';

const ExpensiveComponent = ({ items }) => {
  // Compute the sum of item values only when 'items' changes
  const total = useMemo(() => {
    console.log('Calculating total...');
    return items.reduce((acc, item) => acc + item.value, 0);
  }, [items]);

  return <div>Total: {total}</div>;
};
```

**`useCallback`:**
- **Purpose:** Caches a function and only recreates it when its dependencies change. This is useful for preventing unnecessary re-renders of child components that rely on reference equality to prevent re-renders.
- **Usage:** Use `useCallback` when you want to avoid recreating a function on every render, especially when passing callbacks to child components.

**Example:**

```jsx
import { useCallback } from 'react';

const ChildComponent = ({ onClick }) => {
  console.log('ChildComponent rendered');
  return <button onClick={onClick}>Click Me</button>;
};

const ParentComponent = () => {
  const handleClick = useCallback(() => {
    console.log('Button clicked');
  }, []);

  return <ChildComponent onClick={handleClick} />;
};
```

### 14. Explain how custom hooks can be used to create custom render logic or higher-order components.

**Custom Hooks for Render Logic:**
Custom hooks can encapsulate complex rendering logic, making it reusable across different components.

**Example:**

```jsx
import { useState } from 'react';

// Custom hook to manage the visibility of a component
const useVisibility = (initialState = false) => {
  const [isVisible, setIsVisible] = useState(initialState);
  const toggleVisibility = () => setIsVisible(prev => !prev);
  return [isVisible, toggleVisibility];
};

// Component using the custom hook
const ToggleComponent = () => {
  const [isVisible, toggleVisibility] = useVisibility();

  return (
    <div>
      <button onClick={toggleVisibility}>Toggle</button>
      {isVisible && <p>Now you see me!</p>}
    </div>
  );
};
```

**Custom Hooks as Higher-Order Components (HOCs):**
Custom hooks can also be used to encapsulate logic similar to HOCs by wrapping or augmenting components with additional functionality.

**Example:**

```jsx
import { useState, useEffect } from 'react';

// Custom hook for authentication logic
const useAuth = () => {
  const [isAuthenticated, setIsAuthenticated] = useState(false);

  useEffect(() => {
    // Mock authentication check
    const checkAuth = () => {
      // Assume user is authenticated for example
      setIsAuthenticated(true);
    };

    checkAuth();
  }, []);

  return isAuthenticated;
};

// Component using the custom hook
const ProtectedComponent = () => {
  const isAuthenticated = useAuth();

  if (!isAuthenticated) {
    return <p>Please log in</p>;
  }

  return <p>Welcome back!</p>;
};
```

### 15. Are you familiar with any libraries or tools that help with managing custom hooks in large projects?

**Libraries and Tools:**
1. **`react-query`**: Provides hooks for data fetching, caching, and synchronization. It simplifies managing server state and side effects.
   - **Example:** 
     ```jsx
     import { useQuery } from 'react-query';

     const fetchUser = async () => {
       const response = await fetch('/api/user');
       return response.json();
     };

     const UserProfile = () => {
       const { data, error, isLoading } = useQuery('user', fetchUser);

       if (isLoading) return <div>Loading...</div>;
       if (error) return <div>Error: {error.message}</div>;

       return <div>{data.name}</div>;
     };
     ```

2. **`recoil`**: A state management library that provides hooks for state management with a focus on simplicity and flexibility.
   - **Example:**
     ```jsx
     import { atom, useRecoilState } from 'recoil';

     const textState = atom({
       key: 'textState',
       default: '',
     });

     const TextInput = () => {
       const [text, setText] = useRecoilState(textState);

       return <input value={text} onChange={(e) => setText(e.target.value)} />;
     };
     ```

3. **`zustand`**: A small, fast, and scalable state management library that uses hooks.
   - **Example:**
     ```jsx
     import create from 'zustand';

     const useStore = create((set) => ({
       count: 0,
       increment: () => set((state) => ({ count: state.count + 1 })),
     }));

     const Counter = () => {
       const { count, increment } = useStore();

       return (
         <div>
           <p>Count: {count}</p>
           <button onClick={increment}>Increment</button>
         </div>
       );
     };
     ```

### 16. Be prepared to discuss a specific custom hook you've created in a previous project and its purpose.

**Example Discussion:**

**Custom Hook for Form Validation:**

In a previous project, I created a custom hook `useFormValidation` to manage form validation and error handling. This hook encapsulated the logic for validating form fields and tracking validation errors.

**Code Example:**

```jsx
import { useState } from 'react';

// Custom hook for form validation
const useFormValidation = (validate) => {
  const [values, setValues] = useState({});
  const [errors, setErrors] = useState({});

  const handleChange = (e) => {
    const { name, value } = e.target;
    setValues({
      ...values,
      [name]: value,
    });
  };

  const handleSubmit = (e) => {
    e.preventDefault();
    const validationErrors = validate(values);
    setErrors(validationErrors);

    if (Object.keys(validationErrors).length === 0) {
      // Submit the form
    }
  };

  return {
    values,
    errors,
    handleChange,
    handleSubmit,
  };
};

export default useFormValidation;
```

**Purpose:**
- **Encapsulated Validation Logic:** Simplified form validation across multiple components.
- **Improved Code Organization:** Moved validation logic out of components, making the codebase cleaner and more maintainable.

### 17. The interviewer might ask you to design a custom hook for a particular scenario during the interview.

**Scenario: Managing User Authentication Status**

**Custom Hook:**

```jsx
import { useState, useEffect } from 'react';

// Custom hook for user authentication
const useAuthStatus = () => {
  const [isAuthenticated, setIsAuthenticated] = useState(false);

  useEffect(() => {
    const checkAuthStatus = async () => {
      try {
        const response = await fetch('/api/auth/status');
        const result = await response.json();
        setIsAuthenticated(result.isAuthenticated);
      } catch (error) {
        console.error('Failed to fetch authentication status', error);
      }
    };

    checkAuthStatus();
  }, []);

  return isAuthenticated;
};

export default useAuthStatus;
```

**Explanation:**
- **Purpose:** Fetch and manage the authentication status of a user.
- **Usage:** Provides a simple API for components to check if a user is authenticated and react accordingly.