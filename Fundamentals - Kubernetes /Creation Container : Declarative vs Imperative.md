#Kubernetes : Fundamentals
---

Let's deploy an Nginx container using both methods.

## Imperative

```bash
  kubectl create deployment mynginx1 --image=nginx
```

## Declarative

```bash
  kubectl create -f deploy-example.yaml
```

## Cleanup

```bash
  kubectl delete deployment mynginx1
  kubectl delete deploy mynginx2
```


## Deploiement exemple

Into file `deploy-example.yaml`

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mynginx2
spec:
  replicas: 1
  selector:
    matchLabels:
      app: nginx
      env: prod
  template:
    metadata:
      labels:
        app: nginx
        env: prod
    spec:
      containers:
      - name: nginx
        image: nginx
        resources:
          requests:
            cpu: 100m
            memory: 128Mi
          limits:
            cpu: 250m
            memory: 256Mi        
        ports:
        - containerPort: 80
```
