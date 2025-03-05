# Docker

## Overview
Docker is a platform for developing, shipping, and running applications in containers.

## Dockerfile
```dockerfile
FROM node:18-alpine

WORKDIR /app

COPY package*.json ./
RUN npm ci --only=production

COPY . .

EXPOSE 3000

USER node

CMD ["node", "server.js"]
```

## Commands
```bash
# Build image
docker build -t myapp:1.0 .

# Run container
docker run -d -p 3000:3000 --name myapp myapp:1.0

# List containers
docker ps
docker ps -a

# Logs
docker logs myapp
docker logs -f myapp

# Stop/Remove
docker stop myapp
docker rm myapp

# Exec into container
docker exec -it myapp sh
```

## Docker Compose
```yaml
version: '3.8'

services:
  app:
    build: .
    ports:
      - "3000:3000"
    environment:
      - NODE_ENV=production
      - DATABASE_URL=postgres://db:5432/mydb
    depends_on:
      - db
    
  db:
    image: postgres:15
    volumes:
      - postgres_data:/var/lib/postgresql/data
    environment:
      POSTGRES_PASSWORD: secret

volumes:
  postgres_data:
```

## Best Practices
1. Use **multi-stage builds**
2. Use **specific image tags**
3. **Minimize layers**
4. **Don't run as root**
5. Use **.dockerignore**

## Resources
- Docker Documentation
