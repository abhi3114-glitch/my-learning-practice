# React.js

## Overview
React is a JavaScript library for building user interfaces, developed by Facebook. It uses a component-based architecture and a virtual DOM for efficient rendering.

## Core Concepts

### Components
```jsx
// Function Component
function Welcome({ name }) {
  return <h1>Hello, {name}!</h1>;
}

// Arrow Function Component
const Greeting = ({ message }) => <p>{message}</p>;

// Component with children
const Card = ({ title, children }) => (
  <div className="card">
    <h2>{title}</h2>
    {children}
  </div>
);
```

### JSX
```jsx
const element = (
  <div className="container">
    <h1>Title</h1>
    <p style={{ color: 'blue', fontSize: '16px' }}>
      Styled paragraph
    </p>
    {items.map(item => (
      <li key={item.id}>{item.name}</li>
    ))}
  </div>
);
```

### Hooks

#### useState
```jsx
import { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);
  
  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>+</button>
      <button onClick={() => setCount(prev => prev - 1)}>-</button>
    </div>
  );
}
```

#### useEffect
```jsx
import { useEffect, useState } from 'react';

function DataFetcher({ url }) {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(true);
  
  useEffect(() => {
    let cancelled = false;
    
    async function fetchData() {
      const response = await fetch(url);
      const json = await response.json();
      if (!cancelled) {
        setData(json);
        setLoading(false);
      }
    }
    
    fetchData();
    
    return () => { cancelled = true; };  // Cleanup
  }, [url]);  // Dependencies
  
  if (loading) return <p>Loading...</p>;
  return <pre>{JSON.stringify(data, null, 2)}</pre>;
}
```

#### useContext
```jsx
import { createContext, useContext, useState } from 'react';

const ThemeContext = createContext();

function ThemeProvider({ children }) {
  const [theme, setTheme] = useState('light');
  
  return (
    <ThemeContext.Provider value={{ theme, setTheme }}>
      {children}
    </ThemeContext.Provider>
  );
}

function ThemedButton() {
  const { theme, setTheme } = useContext(ThemeContext);
  
  return (
    <button onClick={() => setTheme(theme === 'light' ? 'dark' : 'light')}>
      Current: {theme}
    </button>
  );
}
```

#### useReducer
```jsx
import { useReducer } from 'react';

const initialState = { count: 0 };

function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return { count: state.count + 1 };
    case 'decrement':
      return { count: state.count - 1 };
    case 'reset':
      return initialState;
    default:
      throw new Error();
  }
}

function Counter() {
  const [state, dispatch] = useReducer(reducer, initialState);
  
  return (
    <>
      Count: {state.count}
      <button onClick={() => dispatch({ type: 'increment' })}>+</button>
      <button onClick={() => dispatch({ type: 'decrement' })}>-</button>
      <button onClick={() => dispatch({ type: 'reset' })}>Reset</button>
    </>
  );
}
```

#### Custom Hooks
```jsx
function useLocalStorage(key, initialValue) {
  const [storedValue, setStoredValue] = useState(() => {
    try {
      const item = window.localStorage.getItem(key);
      return item ? JSON.parse(item) : initialValue;
    } catch (error) {
      return initialValue;
    }
  });
  
  const setValue = (value) => {
    setStoredValue(value);
    window.localStorage.setItem(key, JSON.stringify(value));
  };
  
  return [storedValue, setValue];
}

function useFetch(url) {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);
  
  useEffect(() => {
    fetch(url)
      .then(res => res.json())
      .then(setData)
      .catch(setError)
      .finally(() => setLoading(false));
  }, [url]);
  
  return { data, loading, error };
}
```

### Event Handling
```jsx
function Form() {
  const [value, setValue] = useState('');
  
  const handleSubmit = (e) => {
    e.preventDefault();
    console.log('Submitted:', value);
  };
  
  return (
    <form onSubmit={handleSubmit}>
      <input
        type="text"
        value={value}
        onChange={(e) => setValue(e.target.value)}
        onFocus={() => console.log('Focused')}
        onBlur={() => console.log('Blurred')}
      />
      <button type="submit">Submit</button>
    </form>
  );
}
```

### Conditional Rendering
```jsx
function ConditionalExample({ isLoggedIn, items }) {
  return (
    <div>
      {isLoggedIn && <UserProfile />}
      {isLoggedIn ? <Logout /> : <Login />}
      {items.length > 0 ? (
        <ItemList items={items} />
      ) : (
        <EmptyState />
      )}
    </div>
  );
}
```

### Performance Optimization
```jsx
import { memo, useMemo, useCallback } from 'react';

// Memoized component
const ExpensiveComponent = memo(({ data }) => {
  return <div>{/* render */}</div>;
});

function Parent() {
  const [count, setCount] = useState(0);
  const [items, setItems] = useState([]);
  
  // Memoized value
  const expensiveValue = useMemo(() => {
    return items.reduce((sum, item) => sum + item.value, 0);
  }, [items]);
  
  // Memoized callback
  const handleClick = useCallback(() => {
    setCount(c => c + 1);
  }, []);
  
  return <ExpensiveComponent onClick={handleClick} />;
}
```

### Refs
```jsx
import { useRef, forwardRef } from 'react';

function TextInput() {
  const inputRef = useRef(null);
  
  const focusInput = () => {
    inputRef.current.focus();
  };
  
  return (
    <>
      <input ref={inputRef} />
      <button onClick={focusInput}>Focus</button>
    </>
  );
}

// Forward ref
const FancyInput = forwardRef((props, ref) => (
  <input ref={ref} className="fancy" {...props} />
));
```

## Best Practices

1. Keep components **small and focused**
2. Use **functional components** with hooks
3. **Lift state up** when needed
4. Use **keys** properly in lists
5. **Memoize** expensive computations
6. Handle **loading and error states**
7. Use **prop-types** or TypeScript for type checking

## Project Structure
```
src/
├── components/
│   ├── common/
│   └── features/
├── hooks/
├── context/
├── utils/
├── services/
└── pages/
```

## Resources
- React Documentation
- React Patterns
- Kent C. Dodds' Blog
