# Kubernetes : Fundamentals

## Deploy the app

```bash
    kubectl apply -f myapp.yaml
```

## Deploy the service

```bash
    kubectl apply -f myservice.yaml
```

## Is the service connected to the pod?

If so, the enpoint will point to the pod IP address.  Get the IP address of the pod:

```bash
    kubectl get po -o wide
```

Then get the service endpoint.  The IP address should match.

```bash
    kubectl get ep myservice
```

## Port forward to the service

```bash
    kubectl port-forward service/myservice 8080:80
```

Open a browser and point to http://localhost:8080

Stop the port forward by typing **Ctrl-C**

## Edit the app YAML file

Change the **app** label to myapp2 and save the file

Deploy the change

```bash
    kubectl apply -f myapp.yaml
```

## Check the endpoint again

```bash
    kubectl get ep myservice
```

## Port forward to the service again

```bash
    kubectl port-forward service/myservice 8080:80
```

Open a browser and point to http://localhost:8080

Stop the port forward by typing **Ctrl-C**

## Cleanup

```bash
    kubectl delete -f myservice.yaml
    kubectl delete -f myapp.yaml
```

## MYAPP config

Into `myapp.yaml` : 

````yaml
apiVersion: v1
kind: Pod
metadata:
  name: myapp-pod
  labels:
    app: myapp
    type: front-end
spec:
  containers:
  - name: nginx-container
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
````

## MYSERVICE config

Into `myservice.yml` : 

```yaml
apiVersion: v1
kind: Service
metadata:
 name: myservice
spec:
  ports:
  - port: 80
    targetPort: 80
  selector:
    app: myapp
    type: front-end
```
