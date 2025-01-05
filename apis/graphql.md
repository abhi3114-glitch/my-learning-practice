# GraphQL

## Overview
GraphQL is a query language for APIs that allows clients to request exactly the data they need.

## Schema Definition
```graphql
type User {
  id: ID!
  name: String!
  email: String!
  posts: [Post!]!
}

type Post {
  id: ID!
  title: String!
  content: String
  author: User!
}

type Query {
  users: [User!]!
  user(id: ID!): User
  posts(limit: Int): [Post!]!
}

type Mutation {
  createUser(input: CreateUserInput!): User!
  updateUser(id: ID!, input: UpdateUserInput!): User
  deleteUser(id: ID!): Boolean!
}

input CreateUserInput {
  name: String!
  email: String!
}
```

## Queries
```graphql
# Get specific fields
query {
  user(id: "123") {
    name
    email
    posts {
      title
    }
  }
}

# With variables
query GetUser($id: ID!) {
  user(id: $id) {
    name
    email
  }
}
```

## Mutations
```graphql
mutation CreateUser($input: CreateUserInput!) {
  createUser(input: $input) {
    id
    name
    email
  }
}
```

## Resolvers (Node.js)
```javascript
const resolvers = {
  Query: {
    users: () => db.users.findAll(),
    user: (_, { id }) => db.users.findById(id),
  },
  Mutation: {
    createUser: (_, { input }) => db.users.create(input),
  },
  User: {
    posts: (user) => db.posts.findByUserId(user.id),
  },
};
```

## Best Practices
1. Use **fragments** for reusable fields
2. Implement **pagination** (cursor-based)
3. Use **DataLoader** to prevent N+1 queries
4. Add **rate limiting** and **query depth limits**

## Resources
- GraphQL Documentation
- Apollo GraphQL
