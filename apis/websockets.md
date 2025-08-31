# WebSockets

## Overview
WebSockets provide full-duplex communication channels over a single TCP connection for real-time applications.

## Server (Node.js)
```javascript
const WebSocket = require('ws');
const wss = new WebSocket.Server({ port: 8080 });

wss.on('connection', (ws) => {
  console.log('Client connected');

  ws.on('message', (message) => {
    console.log('Received:', message);
    ws.send(`Echo: ${message}`);
  });

  ws.on('close', () => console.log('Client disconnected'));
});

// Broadcast to all clients
function broadcast(data) {
  wss.clients.forEach((client) => {
    if (client.readyState === WebSocket.OPEN) {
      client.send(data);
    }
  });
}
```

## Client (Browser)
```javascript
const ws = new WebSocket('ws://localhost:8080');

ws.onopen = () => {
  console.log('Connected');
  ws.send('Hello Server!');
};

ws.onmessage = (event) => {
  console.log('Received:', event.data);
};

ws.onclose = () => console.log('Disconnected');
ws.onerror = (error) => console.error('Error:', error);
```

## Socket.IO (Higher-level abstraction)
```javascript
// Server
const io = require('socket.io')(3000);

io.on('connection', (socket) => {
  socket.on('chat message', (msg) => {
    io.emit('chat message', msg);  // Broadcast
  });

  socket.join('room1');
  socket.to('room1').emit('message', 'Hello room!');
});

// Client
const socket = io('http://localhost:3000');
socket.emit('chat message', 'Hello!');
socket.on('chat message', (msg) => console.log(msg));
```

## Use Cases
- Real-time chat
- Live notifications
- Collaborative editing
- Gaming
- Live data feeds

## Best Practices
1. Implement **heartbeat/ping-pong**
2. Handle **reconnection** gracefully
3. Use **rooms/channels** for grouping
4. Add **authentication** on connection

## Resources
- WebSocket API (MDN)
- Socket.IO Documentation
