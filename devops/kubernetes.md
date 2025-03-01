# Kubernetes

## Overview
Kubernetes (K8s) is a container orchestration platform for automating deployment, scaling, and management of containerized applications.

## Key Concepts
- **Pod**: Smallest deployable unit
- **Service**: Network endpoint
- **Deployment**: Manages replicas
- **ConfigMap/Secret**: Configuration
- **Ingress**: External access

## Deployment
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp
spec:
  replicas: 3
  selector:
    matchLabels:
      app: myapp
  template:
    metadata:
      labels:
        app: myapp
    spec:
      containers:
      - name: myapp
        image: myapp:1.0
        ports:
        - containerPort: 3000
        resources:
          limits:
            memory: "256Mi"
            cpu: "500m"
```

## Service
```yaml
apiVersion: v1
kind: Service
metadata:
  name: myapp-service
spec:
  selector:
    app: myapp
  ports:
  - port: 80
    targetPort: 3000
  type: LoadBalancer
```

## Commands
```bash
kubectl apply -f deployment.yaml
kubectl get pods
kubectl get services
kubectl logs pod-name
kubectl exec -it pod-name -- sh
kubectl scale deployment myapp --replicas=5
```

## Best Practices
1. Use **resource limits**
2. Implement **health checks**
3. Use **namespaces**
4. Store secrets in **Secrets**

## Resources
- Kubernetes Documentation
