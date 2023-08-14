# Kubernetes : Fundamentals

Let's now use the Job template.

## Create the Job

```bash
    kubectl apply -f job.yaml
```

## Get the jobs list

```bash
    kubectl get jobs
```

## Get more info

```bash
    kubectl describe job
```

## Get the pod name

Get the pod's log.  Something starting with **hello-**

```bash
    kubectl get pods
```

## Get the jobs list

Get the container's log.  You should see **Hello from the Job**.

```bash
    kubectl logs <podName>
```

## Cleanup

```bash
    kubectl delete -f job.yaml
```

The `job.yaml` file content :

```yaml
apiVersion: batch/v1
kind: Job
metadata:
  name: hello
spec:
  template:
    spec:
      containers:
      - name: busybox
        image: busybox
        command: ["echo", "Hello from the Job"]
      restartPolicy: Never
```
