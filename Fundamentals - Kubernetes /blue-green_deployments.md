**NOTE: If you are running this lab on a ARM64 laptop/PC, edit the YAML file and change the image name from "hello-app" to "hello-arm" keeping the tag name as is.**

## Create a V1 Deployment

    kubectl create -f hello-dep-v1.yaml

## Create the ClusterIP service

    kubectl create -f clusterip.yaml

## Get the pods list

    kubectl get pods -o wide

## Display the app in a browser

First, port forward to the ClusterIP:

    kubectl port-forward service/svc-front 8080:8080

Open a browser and navigate to http://localhost:8080

The app version will be V1.

---

## Create a V2 Deployment

    kubectl create -f hello-dep-v2.yaml

## Get the pods list

    kubectl get pods -o wide

## Edit the ClusterIP manifest

Edit the clusterip.yaml file and change the last line so that the service points to our V2 deployment.

    app: hello-v2

## Update the ClusterIP service

    kubectl apply -f clusterip.yaml

## Display the app in a browser

First, port forward to the ClusterIP:

    kubectl port-forward service/svc-front 8080:8080

Open a browser and navigate to http://localhost:8080

The app version will be V2.

## Cleanup

    kubectl delete -f hello-dep-v1.yaml
    kubectl delete -f hello-dep-v2.yaml
    kubectl delete -f clusterip.yaml

The `clusterip.yaml` file content :

```yml
apiVersion: v1
kind: Service
metadata:
 name: svc-front
spec:
  ports:
  - port: 8080
    targetPort: 8080
  selector:
    app: hello-v1
```

The `hello-dep-v1.yaml` file content :

```yml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: hello-v1
spec:
  replicas: 3
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxSurge: 1
      maxUnavailable: 1
  selector:
    matchLabels:
      app: hello-v1
  template:
    metadata:
      labels:
        app: hello-v1
    spec:
      containers:
      - image: guybarrette/hello-app:1.0
        resources:
          requests:
            cpu: 100m
            memory: 128Mi
          limits:
            cpu: 250m
            memory: 256Mi      
        imagePullPolicy: Always
        name: hello-v1
        ports:
        - containerPort: 8080
```

The `hello-dep-v2.yaml` file content :

```yml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: hello-v2
spec:
  replicas: 3
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxSurge: 1
      maxUnavailable: 1
  selector:
    matchLabels:
      app: hello-v2
  template:
    metadata:
      labels:
        app: hello-v2
    spec:
      containers:
      - image: guybarrette/hello-app:2.0
        resources:
          requests:
            cpu: 100m
            memory: 128Mi
          limits:
            cpu: 250m
            memory: 256Mi      
        imagePullPolicy: Always
        name: hello-v2
        ports:
        - containerPort: 8080
```


Source : https://github.com/K8sAcademy/Fundamentals-HandsOn/tree/main/L25-04%20Blue-Green%20Deployments
