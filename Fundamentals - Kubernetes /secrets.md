#  Kubernetes : Fundamentals

To quickly encode/decode strings into base64

    https://www.base64encode.org/
    https://www.base64decode.org/

or on Windows, install base64

    choco install base64

on Linux/Mac

    echo [string] | base64
    echo [encodedString] | base64 -d

## Create the Secrets

    kubectl apply -f secrets.yaml

## Look at the secrets

    kubectl get secret
    kubectl describe secret secrets
    kubectl get secret secrets -o YAML

## Deploy the pod

    kubectl apply -f pod.yaml

## Connect to the Busybox

    kubectl exec mybox -it -- /bin/sh

## Display the USERNAME and PASSWORD env variables

    echo $USERNAME
    echo $PASSWORD
    exit

## Cleanup

    kubectl delete -f secrets.yaml
    kubectl delete -f pod.yaml --force --grace-period=0

The `pod.yaml` file content : 

````yaml
apiVersion: v1
kind: Pod
metadata:
  name: mybox
spec:
  restartPolicy: Always
  containers:
  - name: mybox
    image: busybox
    resources:
      requests:
        cpu: 100m
        memory: 128Mi
      limits:
        cpu: 250m
        memory: 256Mi    
    command:
      - sleep
      - "3600"
    env:
      - name: USERNAME
        valueFrom:
          secretKeyRef:
            name: secrets
            key: username
      - name: PASSWORD
        valueFrom:
          secretKeyRef:
            name: secrets
            key: password  
````

The `secrets.yaml` file content : 

````yaml
apiVersion: v1
kind: Secret
metadata:
  name: secrets
type: Opaque
data:
  username: VGhlVXNlck5hbWU=
  password: bXlwYXNzd29yZA==
````
