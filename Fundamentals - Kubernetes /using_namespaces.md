# Kubernetes : Fundamentals

## Get namespaces

- Open a terminal and get the currently configured namespaces.

```bash
    kubectl get namespaces
    kubectl get ns
```

## Get the pods list

- Get a list of all the installed pods.

```bash
    kubectl get pods
```

- You get the pods from the default namespace.  Try getting the pods from the docker namespace.  You will get a different list.

```bash
    kubectl get pods --namespace=kube-system
    kubectl get pods -n kube-system
```

## Change namespace

- Change the namespace to the docker one and get the pods list.

```bash
    kubectl config set-context --current --namespace=kube-system
```

## Get the pods

```bash
    kubectl get pods
```

## Now change back to the default namespace

```bash
    kubectl config set-context --current --namespace=default
    kubectl get pods
```

## Create and delete a namespace

```bash
    kubectl create ns [name]
    kubectl get ns
    kubectl delete ns [name]
```
