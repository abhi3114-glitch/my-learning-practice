# Express.js

## Overview
Express is a minimal and flexible Node.js web application framework providing robust features for web and mobile applications.

## Basic Setup
```javascript
const express = require('express');
const app = express();

// Middleware
app.use(express.json());
app.use(express.urlencoded({ extended: true }));

// Routes
app.get('/', (req, res) => res.send('Hello World'));

app.listen(3000, () => console.log('Server on :3000'));
```

## Routing

```javascript
// Basic routes
app.get('/users', getUsers);
app.post('/users', createUser);
app.put('/users/:id', updateUser);
app.delete('/users/:id', deleteUser);

// Route parameters
app.get('/users/:id', (req, res) => {
  const { id } = req.params;
  res.json({ userId: id });
});

// Query parameters
app.get('/search', (req, res) => {
  const { q, page = 1 } = req.query;
  res.json({ query: q, page });
});

// Router modules
const userRouter = express.Router();
userRouter.get('/', getUsers);
userRouter.post('/', createUser);
app.use('/api/users', userRouter);
```

## Middleware

```javascript
// Custom middleware
const logger = (req, res, next) => {
  console.log(`${req.method} ${req.path}`);
  next();
};

app.use(logger);

// Error handling middleware
app.use((err, req, res, next) => {
  console.error(err.stack);
  res.status(500).json({ error: 'Something went wrong!' });
});

// Async error wrapper
const asyncHandler = (fn) => (req, res, next) =>
  Promise.resolve(fn(req, res, next)).catch(next);

app.get('/users', asyncHandler(async (req, res) => {
  const users = await User.findAll();
  res.json(users);
}));
```

## Request & Response

```javascript
// Request object
req.body       // POST body
req.params     // URL parameters
req.query      // Query string
req.headers    // Request headers
req.cookies    // Cookies

// Response methods
res.send('text');
res.json({ data: 'value' });
res.status(201).json({ created: true });
res.redirect('/login');
res.render('template', { data });
res.sendFile('/path/to/file');
res.download('/path/to/file');
```

## Common Middleware

```javascript
const cors = require('cors');
const helmet = require('helmet');
const morgan = require('morgan');
const compression = require('compression');

app.use(cors());
app.use(helmet());
app.use(morgan('combined'));
app.use(compression());
```

## Best Practices

1. Use **Router** for modular routes
2. Implement **error handling** middleware
3. Use **async/await** with error wrapper
4. Add **security middleware** (helmet, cors)
5. Validate **input** with libraries (Joi, express-validator)
6. Structure project with **MVC pattern**

## Resources
- Express.js Documentation
- Express.js Best Practices
