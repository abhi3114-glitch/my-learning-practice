# MongoDB

## Overview
MongoDB is a document-oriented NoSQL database designed for scalability and flexibility with JSON-like documents.

## Basic Operations
```javascript
// Insert
db.users.insertOne({ name: "John", age: 30 });
db.users.insertMany([{ name: "Jane" }, { name: "Bob" }]);

// Find
db.users.find({});
db.users.findOne({ name: "John" });
db.users.find({ age: { $gte: 25 } });

// Update
db.users.updateOne({ name: "John" }, { $set: { age: 31 } });
db.users.updateMany({}, { $inc: { age: 1 } });

// Delete
db.users.deleteOne({ name: "John" });
db.users.deleteMany({ age: { $lt: 18 } });
```

## Query Operators
```javascript
// Comparison
{ age: { $eq: 25 } }
{ age: { $ne: 25 } }
{ age: { $gt: 25 } }
{ age: { $gte: 25 } }
{ age: { $lt: 25 } }
{ age: { $lte: 25 } }
{ age: { $in: [25, 30] } }

// Logical
{ $and: [{ age: { $gt: 25 } }, { active: true }] }
{ $or: [{ age: { $lt: 18 } }, { age: { $gt: 65 } }] }
{ active: { $not: { $eq: false } } }
```

## Aggregation
```javascript
db.orders.aggregate([
  { $match: { status: "completed" } },
  { $group: { _id: "$customerId", total: { $sum: "$amount" } } },
  { $sort: { total: -1 } },
  { $limit: 10 }
]);
```

## Indexes
```javascript
db.users.createIndex({ email: 1 }, { unique: true });
db.users.createIndex({ name: "text" });  // Text search
db.locations.createIndex({ location: "2dsphere" });  // Geospatial
```

## Mongoose (Node.js ODM)
```javascript
const mongoose = require('mongoose');

const userSchema = new mongoose.Schema({
  name: { type: String, required: true },
  email: { type: String, unique: true },
  createdAt: { type: Date, default: Date.now }
});

const User = mongoose.model('User', userSchema);

const user = await User.findById(id);
const users = await User.find({ age: { $gte: 18 } }).limit(10);
await User.findByIdAndUpdate(id, { name: "New Name" });
```

## Best Practices
1. Use **indexes** for frequently queried fields
2. Design **schema** based on access patterns
3. Use **aggregation** for complex queries
4. Implement **data validation**

## Resources
- MongoDB Documentation
- Mongoose Documentation
