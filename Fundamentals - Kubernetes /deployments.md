# Kubernetes : Fundamentals

Let's now use the Deployment template instead of the Pod template.

## Create the Deployment

```bash
    kubectl apply -f deploy-example.yaml
```

## Get the pods list

```bash
    kubectl get pods -o wide
```

## Describe the pod

```bash
    kubectl describe pod deploy-example
```

## Get the Deployment info

```bash
    kubectl get deploy
    kubectl describe deploy deploy-example
```

## Get the ReplicaSet name

```bash
    kubectl get rs
```

## Describe the ReplicaSet

```bash
    kubectl describe rs
```

## Cleanup

```bash
    kubectl delete -f deploy-example.yaml
```

Into ``deploy-example.yaml` File

```yml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: deploy-example
spec:
  replicas: 3
  revisionHistoryLimit: 3
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
        image: nginx:alpine
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
