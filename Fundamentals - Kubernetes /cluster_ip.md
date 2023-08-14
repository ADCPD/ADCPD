# Kubernetes : Fundamentals


## Deploy the service

    kubectl apply -f clusterip.yaml

## Deploy the app

    kubectl apply -f deploy-app.yaml

## Deploy Busybox

    kubectl apply -f pod.yaml

## Get the pods list

    kubectl get pods -o wide

## Connect to the BusyBox container

    kubectl exec mybox -it -- /bin/sh

## Get the Nginx home page thru the ClusterIP service

    wget -qO- http://svc-example:8080
    exit

## Cleanup

    kubectl delete -f clusterip.yaml
    kubectl delete -f deploy-app.yaml
    kubectl delete -f pod.yaml --grace-period=0 --force


The `clusterip.yaml` file content :

```yaml
apiVersion: v1
kind: Service
metadata:
 name: svc-example
spec:
  ports:
  - port: 8080
    targetPort: 80
  selector:
    app: app-example
    env: prod
```

The `deploy-app.yaml` file content :

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: deploy-example
spec:
  replicas: 3
  revisionHistoryLimit: 3
  selector:
    matchLabels:
      app: app-example
      env: prod
  template:
    metadata:
      labels:
        app: app-example
        env: prod
    spec:
      containers:
      - name: nginx
        image: nginx:alpine
        ports:
        - containerPort: 80
```

The `pod.yaml` file content :

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: mybox
spec:
  restartPolicy: Always
  containers:
  - name: mybox
    image: busybox
    resources:
      requests:
        cpu: 100m
        memory: 128Mi
      limits:
        cpu: 250m
        memory: 256Mi    
    command:
      - sleep
      - "3600"
```
