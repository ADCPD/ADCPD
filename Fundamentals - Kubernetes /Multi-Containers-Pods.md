# Kubernetes : Fundamentals

Let’s create multiple containers in a Pod using a YAML file.  We'll use the Busybox container to get the default page served by the Nginx container.

## Create the pod

```bash
    kubectl create -f two-containers.yaml
```

## Get some info

```bash
    kubectl get pods -o wide
    kubectl describe pod two-containers
```

## Connect to the BusyBox container

```bash
    kubectl exec -it two-containers --container mybox -- /bin/sh
```

## Fetch the HTML page served by the Nginx container

This will output the content of the Web page in the terminal.

```bash
    wget -qO- localhost
```

## Quit

```bash
    exit
```

## Cleanup

```bash
    kubectl delete -f two-containers.yaml --force --grace-period=0
```

## `two-containers.yaml` config file 

````yaml
apiVersion: v1
kind: Pod
metadata:
  name: two-containers
spec:
  restartPolicy: Always
  containers:
  - name: mynginx
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
  - name: mybox
    image: busybox
    resources:
      requests:
        cpu: 100m
        memory: 128Mi
      limits:
        cpu: 250m
        memory: 256Mi    
    ports:
      - containerPort: 81
    command:
      - sleep
      - "3600"
````
