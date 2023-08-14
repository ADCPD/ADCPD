# Kubernetes - Fundamentals 

Let's use an Init container.

## Create the deployment

````bash
    kubectl apply -f myapp.yaml
````

Wait for the main pod to come up

````bash
    kubectl get pods
````

## Connect to the Nginx container

````bash
    kubectl exec -it init-demo -- /bin/bash
````
## Hit the default webpage

It should be the one downloaded by the Init container from http://info.cern.ch

````bash
    curl localhost
    exit
````

## Cleanup

````bash
    kubectl delete -f myapp.yaml
````

## MYAPP FILE `YML` config 

Into the ``myapp.yaml` file :

````yaml
apiVersion: v1
kind: Pod
metadata:
  name: init-demo
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
    volumeMounts:
    - name: workdir
      mountPath: /usr/share/nginx/html
  initContainers:
  - name: install
    image: busybox
    command:
    - wget
    - "-O"
    - "/work-dir/index.html"
    - http://info.cern.ch
    volumeMounts:
    - name: workdir
      mountPath: "/work-dir"
  volumes:
  - name: workdir
    emptyDir: {}
````
