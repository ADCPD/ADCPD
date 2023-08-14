# Kubernetes : Fundamentals

Let’s first create a node running Nginx by using the imperative way.

## Create the pod

```bash
    kubectl run mynginx --image=nginx
```

## Get a list of running pods

```bash
    kubectl get pods
```

## Get more info

```bash
    kubectl get pods -o wide
    kubectl describe pod mynginx
```

## Delete the pod

```bash
    kubectl delete pod mynginx
```

## Create a pod running BusyBox

Let’s now create a node running BusyBox, this time attaching bash to our terminal.

```bash
    kubectl run mybox --image=busybox -it -- /bin/sh
```

## List the folders and use command

```bash
    ls
    echo -n 'A Secret' | base64
    exit
```

## Cleanup

```bash
    kubectl delete pod mybox
```

## Create a pod using the declarative way

Let’s now create a node using a YAML file.

```bash
    kubectl create -f myapp.yaml
```

## Get some info

```bash
    kubectl get pods -o wide
    kubectl describe pod myapp-pod
```

## Attach our terminal

```bash
    kubectl exec -it myapp-pod -- bash
```
Print the DBCON environment variable that was set in the YAML file.

```bash
    echo $DBCON
```

## Detach from the instance

```bash
    exit
```

## Cleanup

```bash
    kubectl delete -f myapp.yaml
```

## MY APP config POD :

Into `myapp.yaml` (exemple):

```yaml
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
      name: http
      protocol: TCP
    env:
    - name: DBCON
      value: myconnectionstring
```
