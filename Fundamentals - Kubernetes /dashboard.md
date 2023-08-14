# Kubernetes : Fundamentals

The `dashboard-clusterrolebinding.yaml` file content :

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: admin-user
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: cluster-admin
subjects:
- kind: ServiceAccount
  name: admin-user
  namespace: kubernetes-dashboard
```

The `dashboard-serviceaccount.yaml` file content :

```yaml
apiVersion: v1
kind: ServiceAccount
metadata:
  name: admin-user
  namespace: kubernetes-dashboard
```

The `hello-deployment.yaml` file content :

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: hello-deploy
  namespace: default
spec:
  replicas: 2
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxSurge: 1
      maxUnavailable: 1
  selector:
    matchLabels:
      app: hello-app
  template:
    metadata:
      labels:
        app: hello-app
    spec:
      containers:
      - image: gcr.io/google-samples/hello-app:1.0
        imagePullPolicy: Always
        resources:
          requests:
            cpu: 50m
            memory: 64Mi
          limits:
            cpu: 100m
            memory: 128Mi 
        name: hello-dep
        ports:
        - containerPort: 80
---
apiVersion: v1
kind: Service
metadata:
 name: hello-svc
spec:
  ports:
  - port: 8080
    targetPort: 80
  selector:
    app: hello-app  
```

The `token.txt` file content :

```text

```
