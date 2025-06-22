# gRPC

## Overview
gRPC is a high-performance RPC framework using Protocol Buffers for efficient serialization.

## Protocol Buffers
```protobuf
// user.proto
syntax = "proto3";

package user;

service UserService {
  rpc GetUser (GetUserRequest) returns (User);
  rpc ListUsers (ListUsersRequest) returns (stream User);
  rpc CreateUser (CreateUserRequest) returns (User);
}

message User {
  int32 id = 1;
  string name = 2;
  string email = 3;
}

message GetUserRequest {
  int32 id = 1;
}
```

## Server (Node.js)
```javascript
const grpc = require('@grpc/grpc-js');
const protoLoader = require('@grpc/proto-loader');

const server = new grpc.Server();

server.addService(userProto.UserService.service, {
  getUser: (call, callback) => {
    const user = findUser(call.request.id);
    callback(null, user);
  }
});

server.bindAsync('0.0.0.0:50051', 
  grpc.ServerCredentials.createInsecure(),
  () => server.start()
);
```

## Client
```javascript
const client = new userProto.UserService(
  'localhost:50051',
  grpc.credentials.createInsecure()
);

client.getUser({ id: 1 }, (error, user) => {
  console.log(user);
});
```

## Benefits
- **Binary protocol** - Faster than JSON
- **Strongly typed** - Schema validation
- **Streaming** - Bi-directional
- **Code generation** - Auto-generate clients

## Resources
- gRPC Documentation
