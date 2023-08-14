#  Kubernetes : Fundamentals

Lens is a free dashboard app that you can install on Windows, Mac and Linux.

## Install Lens

Directly from the Lens Web site or...

Windows (if you have Chocolatey installed):

    choco install lens

macOS (if you have Brew installed):

    brew install --cask lens

Linux: see https://k8slens.dev/

## Launch Lens

You should be connected to your cluster on (1) Docker Desktop.  If not, you can add it or another cluster by (2) clicking on the **hamburger menu** and (3) **Add Cluster**.

The clusters that are already present in the config file will be listed in the dropdown menu.

Once configured, you should see something like this:


## Deploy the app

    kubectl create -f hello-deployment.yaml

## Lens dashboard

Open the **Workloads** menu and look at the pods, deployments and replications.

## Delete a pod using the UI

Select one of the pods and delete it either by clicking on the (2) **ellipse** icon or the (2) **Delete** icon at the bottom of the screen.  You'll notice that the pod will be replaced almost immediately.

## Open a terminal

At the bottom of the screen, you will see a link called **Terminal**.  Click on it to open the built-in terminal.

## Delete a pod using the terminal

Copy one of the pod name and delete it using the terminal.

    kubectl delete pod [podName]

## Cleanup

    kubectl delete -f hello-deployment.yaml


The `hello-deployment.yaml` file content :

````yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: hello-dep
  namespace: default
spec:
  replicas: 3
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxSurge: 1
      maxUnavailable: 1
  selector:
    matchLabels:
      app: hello-dep
  template:
    metadata:
      labels:
        app: hello-dep
    spec:
      containers:
      - image: gcr.io/google-samples/hello-app:1.0
        name: hello-dep
        ports:
        - containerPort: 8080
````
