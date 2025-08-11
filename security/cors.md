# CORS (Cross-Origin Resource Sharing)

## Overview
CORS is a security feature that restricts web pages from making requests to a different domain than the one serving the page.

## Headers
```http
Access-Control-Allow-Origin: https://example.com
Access-Control-Allow-Methods: GET, POST, PUT, DELETE
Access-Control-Allow-Headers: Content-Type, Authorization
Access-Control-Allow-Credentials: true
Access-Control-Max-Age: 86400
```

## Express.js Setup
```javascript
const cors = require('cors');

// Allow all origins
app.use(cors());

// Specific configuration
app.use(cors({
  origin: ['https://example.com', 'https://app.example.com'],
  methods: ['GET', 'POST', 'PUT', 'DELETE'],
  allowedHeaders: ['Content-Type', 'Authorization'],
  credentials: true,
  maxAge: 86400
}));

// Dynamic origin
app.use(cors({
  origin: (origin, callback) => {
    const allowed = ['https://example.com'];
    if (!origin || allowed.includes(origin)) {
      callback(null, true);
    } else {
      callback(new Error('Not allowed by CORS'));
    }
  }
}));
```

## Preflight Requests
```
OPTIONS /api/users
Origin: https://example.com
Access-Control-Request-Method: POST
Access-Control-Request-Headers: Content-Type
```

## Best Practices
1. **Whitelist** specific origins in production
2. Don't use `*` with **credentials**
3. Set appropriate **max-age** for preflight caching

## Resources
- MDN CORS Guide
