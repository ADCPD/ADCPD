# Kubernetes : Fundamentals

Let's now use the ReplicaSet template instead of the Pod template.

## Create the ReplicaSet

```bash
    kubectl apply -f rs-example.yaml
```

## Get the pods list

```bash
    kubectl get pods -o wide
```

## Get the ReplicaSet name

```bash
    kubectl get rs
```

## Describe the ReplicaSet

```bash
    kubectl describe rs rs-example
```

## Cleanup

```bash
    kubectl delete -f rs-example.yaml
```

## `rs-example.yaml` config

Into the file :

```yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
 name: rs-example
spec:
 replicas: 3
 selector:
   matchLabels:
     app: nginx
     type: front-end
 template: 
   metadata:
     labels:
       app: nginx
       type: front-end
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
