# Kubernetes : Fundamentals

Let's deploy a Busybox as a DaemonSet.

## Create the Deployment

```bash
    kubectl apply -f daemonset.yaml
```

## Get the pods list

There should be one for each worker node.

```bash
    kubectl get pods --selector=app=daemonset-example -o wide
```

## Cleanup

```bash
    kubectl delete -f daemonset.yaml
```

Into the `daemonset.yaml` file :

````yaml
apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: daemonset-example
  labels:
    app: daemonset-example
spec:
  selector:
    matchLabels:
      app: daemonset-example
  template:
    metadata:
      labels:
        app: daemonset-example
    spec:
      tolerations:
      - key: node-role.kubernetes.io/master
        effect: NoSchedule
      containers:
      - name: busybox
        image: busybox
        args:
        - sleep
        - "10000"
````
