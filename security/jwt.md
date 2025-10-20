# JWT (JSON Web Tokens)

## Overview
JWT is a compact, URL-safe token format for securely transmitting information between parties as a JSON object.

## Structure
```
Header.Payload.Signature

eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.
eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4ifQ.
SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c
```

## Creating Tokens (Node.js)
```javascript
const jwt = require('jsonwebtoken');

const token = jwt.sign(
  { userId: 123, role: 'admin' },
  process.env.JWT_SECRET,
  { expiresIn: '24h' }
);
```

## Verifying Tokens
```javascript
try {
  const decoded = jwt.verify(token, process.env.JWT_SECRET);
  console.log(decoded.userId);
} catch (error) {
  console.log('Invalid token');
}
```

## Middleware
```javascript
const authMiddleware = (req, res, next) => {
  const token = req.headers.authorization?.split(' ')[1];
  
  if (!token) {
    return res.status(401).json({ error: 'No token provided' });
  }
  
  try {
    req.user = jwt.verify(token, process.env.JWT_SECRET);
    next();
  } catch {
    res.status(401).json({ error: 'Invalid token' });
  }
};
```

## Best Practices
1. Use **strong secrets** (256+ bits)
2. Set **short expiration** times
3. Use **HTTPS** only
4. Store in **httpOnly cookies** for web
5. Implement **refresh tokens** for long sessions

## Resources
- JWT.io
