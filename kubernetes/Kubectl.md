# GUIDE TO USE kubernetes - Kubectl 

- Afficher les cluters de travail 

```
kubectl config get-contexts
```

- Changer le cluster de travail 

```
kubectl config use villagile-int
```

-  La liste des namespaces :

```
kubectl get namespaces
```

ou bien

```
kubectl get ns
```

-  Remplacer le namespace :

```
kubectl config set-context --current --namespace=zeus-int
```

-  Remplacer le namespace :

```
kubectl config set-context --current --namespace=zeus-int
```

-  Verifier si le nouveau namespace est pris en compte :

```
  kubectl config view --minify | grep namespace:
```

- Pour avoir la liste des pods du namespace `zeus-int`

```
  kubectl -n zeus-int get po
```

- pour avoir la liste des pods du namespace `user-request-int`

```
  kubectl -n user-request-int get po 
```

- Accèder à un `POD` :
    `vdm-msd-api-symfony-bc4f8d4fb-66l7h` peut changer

```
    k -n zeus-int exec -it  vdm-msd-api-symfony-bc4f8d4fb-66l7h -- bash
```

- Visualiser les logs d'un `POD`

```
    kubectl logs vdm-msd-api-symfony-bc4f8d4fb-66l7h
```

- pour avoir la liste des services associée au namespace `zeus-int`

```
  kubectl -n zeus-int get svc 
```

- pour avoir la liste des ingress(DNS)

```
  kubectl -n zeus-int get ingress  
```

- pour avoir la liste des images

```
  kubectl -n zeus-int get deployment   
```



# FICHIER CONFIG INFRA (MSD-VDM)

- chercher le fichier conf dans infra 
```
k get deploy -n zeus-int

// retourner la lister des pods deployer 
k get deploy -n zeus-int

// modifier le fichier manuellement 
k  edit vdm-msd-api-symfony

// modifier le fichier deployer
k  edit deploy -n zeus-int vdm-msd-api-symfony
```

 
