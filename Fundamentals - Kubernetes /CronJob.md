# Kubernetes : Fundamentals

Let's now use the CronJob template.

## Create the Job

```bash
    kubectl apply -f cronjob.yaml
```

## Get the jobs list

```bash
    kubectl get cronjobs
```

## Get more info

```bash
    kubectl describe cronjob
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
    kubectl delete -f cronjob.yaml
```

The `cronjob.yaml`FIle content : 

```yaml
apiVersion: batch/v1
kind: CronJob
metadata:
  name: hello-cron
spec:
  schedule: "* * * * *"
  jobTemplate:
    spec:
      template:
        spec:
          containers:
          - name: busybox
            image: busybox
            command: ["echo", "Hello from the CronJob"]
          restartPolicy: Never
```
