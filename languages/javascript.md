# JavaScript

## Overview
JavaScript is a high-level, interpreted programming language that conforms to the ECMAScript specification. It is a dynamic, weakly typed, prototype-based language with first-class functions.

## Core Concepts

### Variables and Data Types
```javascript
// Variable declarations
let name = "John";        // Block-scoped, reassignable
const PI = 3.14159;       // Block-scoped, constant
var oldStyle = "avoid";   // Function-scoped (legacy)

// Data Types
const string = "Hello";
const number = 42;
const boolean = true;
const nullValue = null;
const undefinedValue = undefined;
const symbol = Symbol("unique");
const bigInt = 9007199254740991n;
const object = { key: "value" };
const array = [1, 2, 3];
```

### Functions
```javascript
// Function Declaration
function greet(name) {
  return `Hello, ${name}!`;
}

// Arrow Functions
const add = (a, b) => a + b;

// Higher-Order Functions
const numbers = [1, 2, 3, 4, 5];
const doubled = numbers.map(n => n * 2);
const evens = numbers.filter(n => n % 2 === 0);
const sum = numbers.reduce((acc, n) => acc + n, 0);
```

### Async Programming
```javascript
// Promises
const fetchData = () => {
  return new Promise((resolve, reject) => {
    setTimeout(() => resolve("Data"), 1000);
  });
};

// Async/Await
async function getData() {
  try {
    const data = await fetchData();
    console.log(data);
  } catch (error) {
    console.error(error);
  }
}

// Promise.all for parallel execution
const results = await Promise.all([
  fetch('/api/users'),
  fetch('/api/posts')
]);
```

### ES6+ Features
```javascript
// Destructuring
const { name, age } = person;
const [first, second, ...rest] = array;

// Spread Operator
const newArray = [...array, 4, 5];
const newObject = { ...object, newKey: "value" };

// Template Literals
const message = `Hello, ${name}! You are ${age} years old.`;

// Classes
class Animal {
  constructor(name) {
    this.name = name;
  }
  
  speak() {
    console.log(`${this.name} makes a sound.`);
  }
}

// Modules
export const helper = () => {};
import { helper } from './utils.js';
```

### Closures
```javascript
function createCounter() {
  let count = 0;
  return {
    increment: () => ++count,
    decrement: () => --count,
    getCount: () => count
  };
}

const counter = createCounter();
counter.increment(); // 1
counter.increment(); // 2
```

### Event Loop
```javascript
console.log('1');           // Sync - First

setTimeout(() => {
  console.log('2');         // Macro task - Last
}, 0);

Promise.resolve().then(() => {
  console.log('3');         // Micro task - Second
});

console.log('4');           // Sync - Third

// Output: 1, 4, 3, 2
```

## Best Practices

1. **Use const by default**, let when reassignment is needed
2. **Avoid var** - it has confusing scoping rules
3. **Use arrow functions** for callbacks
4. **Handle errors** in async code with try/catch
5. **Use destructuring** for cleaner code
6. **Avoid mutation** - prefer immutable patterns
7. **Use template literals** instead of string concatenation

## Common Patterns

### Module Pattern
```javascript
const Module = (function() {
  const private = "I'm private";
  
  return {
    getPrivate: () => private
  };
})();
```

### Debounce
```javascript
function debounce(fn, delay) {
  let timeoutId;
  return function(...args) {
    clearTimeout(timeoutId);
    timeoutId = setTimeout(() => fn.apply(this, args), delay);
  };
}
```

### Throttle
```javascript
function throttle(fn, limit) {
  let inThrottle;
  return function(...args) {
    if (!inThrottle) {
      fn.apply(this, args);
      inThrottle = true;
      setTimeout(() => inThrottle = false, limit);
    }
  };
}
```

## Resources
- MDN Web Docs
- JavaScript.info
- You Don't Know JS (book series)
