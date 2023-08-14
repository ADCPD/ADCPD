#Kubernetes : Fundamentals
---

Let's deploy an Nginx container using both methods.

## Imperative

```bash
  kubectl create deployment mynginx1 --image=nginx
```

## Declarative

```bash
  kubectl create -f deploy-example.yaml
```

## Cleanup

```bash
  kubectl delete deployment mynginx1
  kubectl delete deploy mynginx2
```
