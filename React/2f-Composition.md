# Composition

### 1. What is component composition in React, and why is it important?

**Component composition** in React is the practice of combining multiple components to build a more complex UI. Instead of creating a single monolithic component, you break down the UI into smaller, reusable components and compose them together.

**Importance:**
- **Reusability:** Smaller components can be reused across different parts of the application.
- **Maintainability:** Code is easier to manage and understand when it's broken down into smaller pieces.
- **Separation of Concerns:** Each component manages its own logic and UI, promoting modularity.

**Example:**

```jsx
// Button.js
const Button = ({ onClick, children }) => (
  <button onClick={onClick}>{children}</button>
);

export default Button;

// App.js
import Button from './Button';

const App = () => (
  <div>
    <h1>Welcome to my app!</h1>
    <Button onClick={() => alert('Clicked!')}>Click Me</Button>
  </div>
);

export default App;
```

### 2. How does component composition differ from traditional templating approaches?

**Traditional templating** often involves using templates with embedded logic or repetitive code directly in the template. React's component composition, on the other hand, abstracts these concerns into reusable components that manage their own state and logic.

**Differences:**
- **Encapsulation:** In React, components encapsulate both structure and behavior. Traditional templates might separate structure and behavior.
- **Reusability:** React components are designed for reuse, while traditional templates often lead to code duplication.
- **Flexibility:** React components can be composed in various ways, offering greater flexibility compared to static templates.

**Example of a traditional templating approach (e.g., Handlebars):**

```handlebars
<!-- template.handlebars -->
<div>
  <h1>{{title}}</h1>
  <button onclick="{{clickHandler}}">Click Me</button>
</div>
```

**React approach (Component Composition):**

```jsx
// Header.js
const Header = ({ title }) => <h1>{title}</h1>;

// Button.js
const Button = ({ onClick, children }) => (
  <button onClick={onClick}>{children}</button>
);

// App.js
import Header from './Header';
import Button from './Button';

const App = () => (
  <div>
    <Header title="Welcome to my app!" />
    <Button onClick={() => alert('Clicked!')}>Click Me</Button>
  </div>
);

export default App;
```

### 3. Explain the benefits of breaking down UI into smaller, reusable components.

**Benefits:**

- **Reusability:** Components can be reused across different parts of the application, reducing duplication.
- **Maintainability:** Smaller components are easier to manage, test, and debug.
- **Readability:** Code is more readable and understandable when divided into smaller, focused components.
- **Isolation:** Components encapsulate their own logic and style, preventing unintended side effects.

**Example:**

```jsx
// Card.js
const Card = ({ title, content }) => (
  <div className="card">
    <h2>{title}</h2>
    <p>{content}</p>
  </div>
);

// Dashboard.js
import Card from './Card';

const Dashboard = () => (
  <div>
    <Card title="Card 1" content="Content of card 1" />
    <Card title="Card 2" content="Content of card 2" />
  </div>
);

export default Dashboard;
```

### 4. How can you leverage props and state within composed components?

**Props** are used to pass data and event handlers from parent to child components, while **state** is used within a component to manage its own data.

**Example:**

```jsx
// ParentComponent.js
import { useState } from 'react';
import ChildComponent from './ChildComponent';

const ParentComponent = () => {
  const [count, setCount] = useState(0);

  return (
    <div>
      <h1>Counter: {count}</h1>
      <ChildComponent count={count} increment={() => setCount(count + 1)} />
    </div>
  );
};

// ChildComponent.js
const ChildComponent = ({ count, increment }) => (
  <div>
    <p>The count is {count}</p>
    <button onClick={increment}>Increment</button>
  </div>
);
```

### 5. Describe a situation where component composition would be a better approach than a single, monolithic component.

**Situation:**

When building a complex form with multiple sections (e.g., personal details, address, and payment information), component composition allows you to break the form into smaller, manageable pieces.

**Example:**

```jsx
// PersonalDetails.js
const PersonalDetails = ({ details, onChange }) => (
  <div>
    <input
      type="text"
      name="name"
      value={details.name}
      onChange={onChange}
      placeholder="Name"
    />
    <input
      type="email"
      name="email"
      value={details.email}
      onChange={onChange}
      placeholder="Email"
    />
  </div>
);

// Address.js
const Address = ({ address, onChange }) => (
  <div>
    <input
      type="text"
      name="street"
      value={address.street}
      onChange={onChange}
      placeholder="Street"
    />
    <input
      type="text"
      name="city"
      value={address.city}
      onChange={onChange}
      placeholder="City"
    />
  </div>
);

// Payment.js
const Payment = ({ payment, onChange }) => (
  <div>
    <input
      type="text"
      name="cardNumber"
      value={payment.cardNumber}
      onChange={onChange}
      placeholder="Card Number"
    />
  </div>
);

// Form.js
import PersonalDetails from './PersonalDetails';
import Address from './Address';
import Payment from './Payment';

const Form = () => {
  const [details, setDetails] = useState({ name: '', email: '' });
  const [address, setAddress] = useState({ street: '', city: '' });
  const [payment, setPayment] = useState({ cardNumber: '' });

  const handleChange = (e) => {
    const { name, value } = e.target;
    if (name in details) {
      setDetails({ ...details, [name]: value });
    } else if (name in address) {
      setAddress({ ...address, [name]: value });
    } else if (name in payment) {
      setPayment({ ...payment, [name]: value });
    }
  };

  return (
    <div>
      <PersonalDetails details={details} onChange={handleChange} />
      <Address address={address} onChange={handleChange} />
      <Payment payment={payment} onChange={handleChange} />
    </div>
  );
};

export default Form;
```

### 6. How can you ensure proper data flow and communication between composed components?

**Data flow and communication** can be managed using **props** to pass data and callbacks from parent to child components. **State lifting** can be used to manage shared state between components.

**Example:**

```jsx
// ParentComponent.js
import { useState } from 'react';
import ChildComponentA from './ChildComponentA';
import ChildComponentB from './ChildComponentB';

const ParentComponent = () => {
  const [sharedState, setSharedState] = useState('Initial Value');

  return (
    <div>
      <ChildComponentA sharedState={sharedState} />
      <ChildComponentB setSharedState={setSharedState} />
    </div>
  );
};

// ChildComponentA.js
const ChildComponentA = ({ sharedState }) => (
  <div>
    <p>Shared State: {sharedState}</p>
  </div>
);

// ChildComponentB.js
const ChildComponentB = ({ setSharedState }) => (
  <div>
    <button onClick={() => setSharedState('Updated Value')}>Update State</button>
  </div>
);
```

### 7. What are some best practices for writing composable components?

**Best Practices:**

1. **Single Responsibility Principle:** Each component should have a single responsibility and handle only one aspect of the UI.
2. **Reusability:** Design components to be reusable and generic so they can be used in multiple places.
3. **Props vs. State:** Use props for passing data and callbacks, and state for managing local component data.
4. **Composition over Inheritance:** Prefer composing components rather than inheriting from one another.
5. **Clear Naming:** Use descriptive names for components and props to make the code more readable.
6. **Separation of Concerns:** Keep logic, styling, and rendering concerns separated.
7. **Testing:** Write tests for components to ensure they behave as expected.

**Example:**

```jsx
// Button.js
const Button = ({ onClick, children, style }) => (
  <button onClick={onClick} style={style}>
    {children}
  </button>
);

// Header.js
const Header = ({ title, subtitle }) => (
  <header>
    <h1>{title}</h1>
    <h2>{subtitle}</h2>
  </header>
);

// App.js
import Button from './Button';
import Header from './Header';

const App = () => (
  <div>
    <Header title="Welcome" subtitle="Glad to have you here!" />
    <Button onClick={() => alert('Button clicked!')} style={{ padding: '10px', backgroundColor: 'blue', color: 'white' }}>
      Click Me
    </Button>
  </div>
);

export default App;
```

### 8. How can you handle complex UI logic using component composition?

**Handling complex UI logic** often involves breaking down the logic into smaller, manageable components and using state and context to manage interactions between them.

**Example:**

Suppose you have a complex form with conditional sections that should only render based on user input:

```jsx
// Form.js
import { useState } from 'react';
import PersonalInfo from './PersonalInfo';
import AddressInfo from './AddressInfo';
import PaymentInfo from './PaymentInfo';

const Form = () => {
  const [step, setStep] = useState('personal'); // 'personal', 'address', 'payment'

  return (
    <div>
      {step === 'personal' && <PersonalInfo onNext={() => setStep('address')} />}
      {step === 'address' && <AddressInfo onNext={() => setStep('payment')} />}
      {step === 'payment' && <PaymentInfo onSubmit={() => alert('Form submitted')} />}
    </div>
  );
};

export default Form;
```

**Component Breakdown:**

```jsx
// PersonalInfo.js
const PersonalInfo = ({ onNext }) => (
  <div>
    <h2>Personal Information</h2>
    {/* Form fields */}
    <button onClick={onNext}>Next</button>
  </div>
);

export default PersonalInfo;

// AddressInfo.js
const AddressInfo = ({ onNext }) => (
  <div>
    <h2>Address Information</h2>
    {/* Form fields */}
    <button onClick={onNext}>Next</button>
  </div>
);

export default AddressInfo;

// PaymentInfo.js
const PaymentInfo = ({ onSubmit }) => (
  <div>
    <h2>Payment Information</h2>
    {/* Form fields */}
    <button onClick={onSubmit}>Submit</button>
  </div>
);

export default PaymentInfo;
```

### 9. Explain the role of Higher-Order Components (HOCs) in component composition.

**Higher-Order Components (HOCs)** are functions that take a component and return a new component with additional props or behavior. They are a pattern for reusing component logic.

**Role:**
- **Code Reuse:** HOCs allow you to reuse logic across multiple components.
- **Separation of Concerns:** They help separate concerns by abstracting out reusable logic from the component itself.
- **Enhanced Functionality:** HOCs can inject additional props or functionality into components.

**Example:**

```jsx
// withAuth.js (HOC)
import React from 'react';

const withAuth = (WrappedComponent) => {
  return class extends React.Component {
    componentDidMount() {
      // Logic for authentication
    }

    render() {
      return <WrappedComponent {...this.props} />;
    }
  };
};

export default withAuth;

// Dashboard.js
import withAuth from './withAuth';

const Dashboard = () => (
  <div>
    <h1>Dashboard</h1>
  </div>
);

export default withAuth(Dashboard);
```

### 10. How can you use custom hooks to promote code reusability across components?

**Custom Hooks** are a way to extract and reuse stateful logic in a function that can be shared across multiple components. They help avoid code duplication and enhance reusability.

**Example:**

Suppose you need to fetch data from an API in multiple components. You can create a custom hook for data fetching:

```jsx
// useFetch.js
import { useState, useEffect } from 'react';

const useFetch = (url) => {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    const fetchData = async () => {
      try {
        const response = await fetch(url);
        const result = await response.json();
        setData(result);
      } catch (err) {
        setError(err);
      } finally {
        setLoading(false);
      }
    };

    fetchData();
  }, [url]);

  return { data, loading, error };
};

export default useFetch;

// UserList.js
import useFetch from './useFetch';

const UserList = () => {
  const { data, loading, error } = useFetch('https://api.example.com/users');

  if (loading) return <div>Loading...</div>;
  if (error) return <div>Error: {error.message}</div>;

  return (
    <ul>
      {data.map(user => (
        <li key={user.id}>{user.name}</li>
      ))}
    </ul>
  );
};

export default UserList;
```

By using `useFetch`, you can easily fetch data in any component without duplicating the fetch logic.

### 11. Discuss potential challenges associated with deep component nesting and how to address them.

**Challenges with Deep Component Nesting:**

1. **Performance Issues:** Deep nesting can lead to performance problems due to unnecessary re-renders, especially if the components are not optimized.

2. **Complexity and Readability:** Deeply nested components can make the code harder to understand and maintain.

3. **Prop Drilling:** Passing data through many layers of components can become cumbersome and error-prone.

**Solutions:**

1. **Use React Context:** React Context can help avoid prop drilling by allowing you to share state across deeply nested components without passing props explicitly.

2. **Component Refactoring:** Break down large components into smaller, more manageable ones. Extract complex logic into custom hooks.

3. **React.memo and useCallback:** Use `React.memo` to prevent unnecessary re-renders and `useCallback` to memoize callback functions.

**Example with Context:**

```jsx
// ThemeContext.js
import { createContext, useContext, useState } from 'react';

const ThemeContext = createContext();

export const ThemeProvider = ({ children }) => {
  const [theme, setTheme] = useState('light');
  return (
    <ThemeContext.Provider value={{ theme, setTheme }}>
      {children}
    </ThemeContext.Provider>
  );
};

export const useTheme = () => useContext(ThemeContext);
```

```jsx
// App.js
import { ThemeProvider, useTheme } from './ThemeContext';

const ThemeSwitcher = () => {
  const { theme, setTheme } = useTheme();
  return (
    <button onClick={() => setTheme(theme === 'light' ? 'dark' : 'light')}>
      Switch to {theme === 'light' ? 'dark' : 'light'} mode
    </button>
  );
};

const AppContent = () => {
  const { theme } = useTheme();
  return (
    <div style={{ background: theme === 'light' ? '#fff' : '#333', color: theme === 'light' ? '#000' : '#fff' }}>
      <h1>{theme === 'light' ? 'Light Mode' : 'Dark Mode'}</h1>
      <ThemeSwitcher />
    </div>
  );
};

const App = () => (
  <ThemeProvider>
    <AppContent />
  </ThemeProvider>
);

export default App;
```

### 12. How can you leverage libraries like React Context to manage shared state across composed components?

**React Context** provides a way to share values (like state) between components without passing props through every level of the component tree.

**Example:**

```jsx
// UserContext.js
import { createContext, useContext, useState } from 'react';

const UserContext = createContext();

export const UserProvider = ({ children }) => {
  const [user, setUser] = useState(null);
  return (
    <UserContext.Provider value={{ user, setUser }}>
      {children}
    </UserContext.Provider>
  );
};

export const useUser = () => useContext(UserContext);
```

```jsx
// Profile.js
import { useUser } from './UserContext';

const Profile = () => {
  const { user } = useUser();
  return user ? <div>Welcome, {user.name}!</div> : <div>Please log in.</div>;
};

export default Profile;
```

```jsx
// App.js
import { UserProvider } from './UserContext';
import Profile from './Profile';

const App = () => (
  <UserProvider>
    <Profile />
  </UserProvider>
);

export default App;
```

### 13. Explain the concept of a "presentational component" and its role in component composition.

**Presentational Component:**

- **Definition:** Presentational components are components primarily concerned with how things look. They receive data and callbacks via props and are responsible for rendering UI.

- **Role in Composition:**
  - **Separation of Concerns:** They separate UI rendering logic from business logic.
  - **Reusability:** They are highly reusable since they are not tied to specific data sources or state management.
  - **Simplicity:** They are simple, focused on display logic, and do not manage state or side effects.

**Example:**

```jsx
// Button.js (Presentational Component)
const Button = ({ onClick, children, style }) => (
  <button onClick={onClick} style={style}>
    {children}
  </button>
);

export default Button;
```

```jsx
// App.js
import Button from './Button';

const App = () => (
  <div>
    <Button onClick={() => alert('Button clicked!')} style={{ padding: '10px', backgroundColor: 'blue', color: 'white' }}>
      Click Me
    </Button>
  </div>
);

export default App;
```

### 14. How can you test composed components effectively to ensure proper functionality?

**Testing Composed Components:**

1. **Unit Testing:** Test individual components in isolation to verify they render correctly and handle props properly.

2. **Integration Testing:** Test how components work together by rendering them in a parent component and simulating user interactions.

3. **Mocking:** Use mocks to simulate external dependencies and isolate the component’s logic.

**Example using React Testing Library:**

```jsx
// App.test.js
import { render, screen, fireEvent } from '@testing-library/react';
import App from './App';

test('renders header and button', () => {
  render(<App />);
  const headerElement = screen.getByText(/Welcome/i);
  expect(headerElement).toBeInTheDocument();
  
  const buttonElement = screen.getByText(/Click Me/i);
  expect(buttonElement).toBeInTheDocument();
});

test('button click triggers alert', () => {
  global.alert = jest.fn(); // Mock the alert function
  render(<App />);
  const buttonElement = screen.getByText(/Click Me/i);
  fireEvent.click(buttonElement);
  expect(global.alert).toHaveBeenCalledWith('Button clicked!');
});
```

### 15. Discuss the trade-offs between using composition versus render props or other patterns for component reusability.

**Composition vs. Render Props vs. Other Patterns:**

1. **Composition:**
   - **Pros:**
     - **Ease of Use:** Simple and intuitive. React’s built-in `children` prop makes composition straightforward.
     - **Performance:** Avoids unnecessary re-renders compared to some other patterns.
   - **Cons:**
     - **Flexibility:** Can become complex if too many nested components are involved.

2. **Render Props:**
   - **Pros:**
     - **Flexibility:** Allows for sharing code and logic between components in a more flexible way.
     - **Dynamic Content:** Can dynamically render different content based on props.
   - **Cons:**
     - **Complexity:** Can introduce “wrapper hell” with deeply nested render props.
     - **Performance:** Potential for performance issues due to extra render cycles.

   **Example:**

   ```jsx
   // DataProvider.js
   const DataProvider = ({ render }) => {
     const data = 'some data';
     return render(data);
   };

   // App.js
   const App = () => (
     <DataProvider render={(data) => <div>{data}</div>} />
   );
   ```

3. **Custom Hooks:**
   - **Pros:**
     - **Reusability:** Encapsulates reusable logic that can be used in multiple components.
     - **Separation of Concerns:** Keeps logic separate from UI rendering.
   - **Cons:**
     - **Learning Curve:** Requires understanding of hooks and their rules.

   **Example:**

   ```jsx
   // useCounter.js
   import { useState } from 'react';

   const useCounter = (initialValue = 0) => {
     const [count, setCount] = useState(initialValue);
     const increment = () => setCount(count + 1);
     const decrement = () => setCount(count - 1);
     return { count, increment, decrement };
   };

   // Counter.js
   import useCounter from './useCounter';

   const Counter = () => {
     const { count, increment, decrement } = useCounter();
     return (
       <div>
         <p>Count: {count}</p>
         <button onClick={increment}>Increment</button>
         <button onClick={decrement}>Decrement</button>
       </div>
     );
   };

   export default Counter;
   ```

**Summary:**

- **Composition** is simple and effective for most use cases but can become complex with deep nesting.
- **Render Props** offer flexibility but may lead to more complex nesting and performance issues.
- **Custom Hooks** provide a clean way to reuse logic without changing the component tree structure but require understanding hooks.