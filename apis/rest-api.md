# REST API

## Overview
REST (Representational State Transfer) is an architectural style for designing networked applications using HTTP methods.

## HTTP Methods
| Method | Purpose | Idempotent |
|--------|---------|------------|
| GET | Retrieve resource | Yes |
| POST | Create resource | No |
| PUT | Update/Replace | Yes |
| PATCH | Partial update | Yes |
| DELETE | Remove resource | Yes |

## Status Codes
```
200 OK - Success
201 Created - Resource created
204 No Content - Success, no body
400 Bad Request - Invalid input
401 Unauthorized - Auth required
403 Forbidden - Not allowed
404 Not Found - Resource not found
409 Conflict - Resource conflict
422 Unprocessable Entity - Validation failed
500 Internal Server Error
```

## Resource Naming
```
GET    /users           - List users
GET    /users/123       - Get user by ID
POST   /users           - Create user
PUT    /users/123       - Update user
DELETE /users/123       - Delete user

# Nested resources
GET    /users/123/orders
POST   /users/123/orders

# Query parameters
GET    /users?page=2&limit=20&sort=name
GET    /products?category=electronics&minPrice=100
```

## Request/Response Format
```json
// Request
POST /api/users
Content-Type: application/json
Authorization: Bearer <token>

{
  "name": "John Doe",
  "email": "john@example.com"
}

// Response
HTTP/1.1 201 Created
Content-Type: application/json

{
  "id": 123,
  "name": "John Doe",
  "email": "john@example.com",
  "createdAt": "2024-01-15T10:30:00Z"
}
```

## Best Practices
1. Use **nouns** for resources, not verbs
2. Use **plural** for collections
3. Return **appropriate status codes**
4. Version your API (`/api/v1/users`)
5. Use **pagination** for lists
6. Include **HATEOAS** links

## Resources
- REST API Tutorial
