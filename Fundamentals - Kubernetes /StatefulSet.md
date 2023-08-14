#  Kubernetes : Fundamentals

Let's now create a StafulSet.

## Create the Deployment

```bash
    kubectl apply -f statefulset.yaml
```

## Get the pods list

```bash
    kubectl get pods -o wide
```

## Get a list of the PersistentVolumes Claims

```bash
    kubectl get pvc
```

## Create a file in nginx-sts-2

Open a session in nginx-sts-2 and create a file in the folder mapped to the volume.

```bash
    kubectl exec nginx-sts-2 -it -- /bin/sh
    cd var/www
    echo Hello > hello.txt
```

## Modify the default Web page

```bash
    cd /usr/share/nginx/html
    cat > index.html
    Hello
    Ctrl-D
    exit
```

## Open a session in nginx-sts-0 and reach nginx-sts-2

```bash
    kubectl exec nginx-sts-0 -it -- /bin/sh
    curl http://nginx-sts-2.nginx-headless
    exit
```

## Delete pod 2

Delete a pod and watch as it is recreated with the same name.

```bash
    kubectl delete pod nginx-sts-2
```

## Is the file still there?

Open a session in nginx-sts-2 and see if the file is still present.

```bash
    kubectl exec nginx-sts-2 -it -- /bin/sh
    ls var/www
    exit
```

## Cleanup

```bash
    kubectl delete -f statefulset.yaml
    kubectl delete pvc www-nginx-sts-0
    kubectl delete pvc www-nginx-sts-1
    kubectl delete pvc www-nginx-sts-2
```

Into the `statefulset.yaml` file :

```yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx-headless
  labels:
    run: nginx-sts-demo
spec:
  ports:
  - port: 80
    name: web
  clusterIP: None
  selector:
    run: nginx-sts-demo
---
apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: nginx-sts
spec:
  serviceName: nginx-headless
  replicas: 3
  selector:
    matchLabels:
      run: nginx-sts-demo
  template:
    metadata:
      labels:
        run: nginx-sts-demo
    spec:
      containers:
      - name: nginx
        image: nginx
        volumeMounts:
        - name: www
          mountPath: /var/www/
  volumeClaimTemplates:
  - metadata:
      name: www
    spec:
      storageClassName: hostpath
      accessModes:
        - ReadWriteOnce
      resources:
        requests:
          storage: 10Mi
```
