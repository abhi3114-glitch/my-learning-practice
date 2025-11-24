# Microservices

## Overview
Microservices architecture structures an application as a collection of loosely coupled, independently deployable services.

## Key Principles
1. **Single Responsibility** - Each service does one thing well
2. **Independence** - Services can be deployed independently
3. **Decentralized** - Each service owns its data
4. **Resilience** - Failure in one service doesn't cascade

## Communication Patterns

### Synchronous (HTTP/gRPC)
```javascript
// Service A calls Service B
const response = await fetch('http://service-b/api/users/123');
```

### Asynchronous (Message Queue)
```javascript
// Producer
await queue.publish('user.created', { userId: 123 });

// Consumer
queue.subscribe('user.created', async (message) => {
  await processNewUser(message.userId);
});
```

## Service Discovery
```yaml
# Kubernetes Service
apiVersion: v1
kind: Service
metadata:
  name: user-service
spec:
  selector:
    app: user-service
  ports:
    - port: 80
      targetPort: 3000
```

## API Gateway Pattern
```
Client -> API Gateway -> Service A
                     -> Service B
                     -> Service C
```

## Circuit Breaker
```javascript
const CircuitBreaker = require('opossum');

const breaker = new CircuitBreaker(riskyFunction, {
  timeout: 3000,
  errorThresholdPercentage: 50,
  resetTimeout: 30000
});

const result = await breaker.fire();
```

## Best Practices
1. Design around **business domains**
2. Use **asynchronous communication** when possible
3. Implement **circuit breakers**
4. Centralize **logging and monitoring**
5. Use **containerization** (Docker/Kubernetes)

## Resources
- Microservices.io
- Building Microservices (book)
