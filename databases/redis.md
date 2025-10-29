# Redis

## Overview
Redis is an in-memory data structure store used as database, cache, message broker, and queue.

## Data Types
```bash
# Strings
SET name "John"
GET name
INCR counter
EXPIRE key 3600

# Lists
LPUSH mylist "item1"
RPUSH mylist "item2"
LRANGE mylist 0 -1
LPOP mylist

# Sets
SADD myset "member1"
SMEMBERS myset
SISMEMBER myset "member1"

# Hashes
HSET user:1 name "John" age 30
HGET user:1 name
HGETALL user:1

# Sorted Sets
ZADD leaderboard 100 "player1"
ZRANGE leaderboard 0 -1 WITHSCORES
ZRANK leaderboard "player1"
```

## Pub/Sub
```bash
SUBSCRIBE channel
PUBLISH channel "message"
```

## Node.js Usage
```javascript
const Redis = require('ioredis');
const redis = new Redis();

await redis.set('key', 'value');
const value = await redis.get('key');

// Caching pattern
async function getUser(id) {
  const cached = await redis.get(`user:${id}`);
  if (cached) return JSON.parse(cached);
  
  const user = await db.findUser(id);
  await redis.setex(`user:${id}`, 3600, JSON.stringify(user));
  return user;
}
```

## Best Practices
1. Use **appropriate data structures**
2. Set **TTL** for cache entries
3. Use **pipelining** for multiple commands
4. Implement **connection pooling**

## Resources
- Redis Documentation
