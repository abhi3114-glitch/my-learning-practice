# Node.js

## Overview
Node.js is a JavaScript runtime built on Chrome's V8 engine. It enables server-side JavaScript execution with non-blocking, event-driven architecture.

## Core Modules

### File System
```javascript
const fs = require('fs');
const fsPromises = require('fs').promises;

// Async (preferred)
const data = await fsPromises.readFile('file.txt', 'utf8');
await fsPromises.writeFile('output.txt', data);

// Sync (blocking)
const content = fs.readFileSync('file.txt', 'utf8');
fs.writeFileSync('output.txt', content);

// Streams
const readable = fs.createReadStream('large.txt');
const writable = fs.createWriteStream('output.txt');
readable.pipe(writable);
```

### HTTP
```javascript
const http = require('http');

const server = http.createServer((req, res) => {
  res.writeHead(200, { 'Content-Type': 'application/json' });
  res.end(JSON.stringify({ message: 'Hello' }));
});

server.listen(3000, () => console.log('Server running on :3000'));
```

### Path
```javascript
const path = require('path');

path.join('/users', 'john', 'docs');  // /users/john/docs
path.resolve('./src', 'index.js');     // Absolute path
path.basename('/path/to/file.txt');    // file.txt
path.extname('file.txt');              // .txt
path.dirname('/path/to/file.txt');     // /path/to
```

### Events
```javascript
const EventEmitter = require('events');

class MyEmitter extends EventEmitter {}
const emitter = new MyEmitter();

emitter.on('event', (data) => console.log(data));
emitter.emit('event', { message: 'Hello' });
```

## Package Management

```bash
# npm
npm init -y
npm install express
npm install -D nodemon
npm run dev

# package.json scripts
{
  "scripts": {
    "start": "node index.js",
    "dev": "nodemon index.js",
    "test": "jest"
  }
}
```

## Environment Variables

```javascript
// .env
require('dotenv').config();

const port = process.env.PORT || 3000;
const dbUrl = process.env.DATABASE_URL;
```

## Error Handling

```javascript
// Async/Await
async function fetchData() {
  try {
    const result = await someAsyncOperation();
    return result;
  } catch (error) {
    console.error('Error:', error.message);
    throw error;
  }
}

// Unhandled rejections
process.on('unhandledRejection', (reason, promise) => {
  console.error('Unhandled Rejection:', reason);
});

// Uncaught exceptions
process.on('uncaughtException', (error) => {
  console.error('Uncaught Exception:', error);
  process.exit(1);
});
```

## Best Practices

1. Use **async/await** over callbacks
2. Handle **errors** properly
3. Use **environment variables**
4. Implement **graceful shutdown**
5. Use **streams** for large files
6. Use a **process manager** (PM2)

## Resources
- Node.js Documentation
- Node.js Best Practices GitHub
