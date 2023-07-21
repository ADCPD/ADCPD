# GUIDE TO USE kubernetes - Kubectl 

```bash
> kcg :  kubectl config get-contexts  # verifier le context / cluster .. env de deploiement
> kc  :  k config get-contexts        # affecter le bon cluster > env
#> tmatlasregistry.azurecr.io :  achercher l\'equivalent dans le fichier jenkinsfile // ou le repo infra
```

helm -n namespace list

### RECUPERER LA LISTE DES ENV DE DEPLOIEMENT 

```bash
#Il faut se rendre dans le repo d'un projet exemple : cd ./atlas/atlas-indicateur-dev-env/atlas-indicateur-frontend
kubectl --namespace=atlas-net-int get deployment

# recupere la liste des deploiement : ce qui existe entre **
#kubectl --namespace=atlas-net-int get deployment **indicateur-frontend-node**  -o jsonpath='{.spec.template.spec.container

kubectl --namespace=atlas-net-int get deployment indicateur-frontend-node  -o jsonpath='{.spec.template.spec.container
```

### RECUPERER LA LISTE DES NAMESPACES

```bash
#Il faut se rendre dans le repo d'un projet exemple : cd ./atlas/atlas-indicateur-dev-env/atlas-indicateur-frontend
helm --namespace=atlas-net-int list | grep indicateur
```

### TROUVER UN POD

- Afficher les cluters de travail 

```bash
kubectl config get-contexts
```

- Changer le cluster de travail 

```bash
kubectl config use villagile-int
```

-  La liste des namespaces :

```bash
kubectl get namespaces
```

ou bien

```bash
kubectl get ns
```

-  Remplacer le namespace :

```bash
kubectl config set-context --current --namespace=zeus-int
```

-  Remplacer le namespace :

```bash
kubectl config set-context --current --namespace=zeus-int
```

-  Verifier si le nouveau namespace est pris en compte :

```bash
  kubectl config view --minify | grep namespace:
```

- Pour avoir la liste des pods du namespace `zeus-int`

```bash
  kubectl -n zeus-int get po
```

- pour avoir la liste des pods du namespace `user-request-int`

```bash
  kubectl -n user-request-int get po 
```

- Accèder à un `POD` :
    `vdm-msd-api-symfony-bc4f8d4fb-66l7h` peut changer

```bash
    k -n zeus-int exec -it  vdm-msd-api-symfony-bc4f8d4fb-66l7h -- bash
```

- Visualiser les logs d'un `POD`

```bash
    kubectl logs vdm-msd-api-symfony-bc4f8d4fb-66l7h
```

- pour avoir la liste des services associée au namespace `zeus-int`

```bash
  kubectl -n zeus-int get svc 
```

- pour avoir la liste des ingress(DNS)

```bash
  kubectl -n zeus-int get ingress  
```

- pour avoir la liste des images

```bash
  kubectl -n zeus-int get deployment   
```

- pour avoir la liste des services

```bash
  kubectl -n zeus-int get service
ou
  kubectl get service
```

# CONFIG POSTGRESQL CONTAINER (MSD-VDM)

```bash
kubectl -n default get po
k -n zeus-int exec -it  postgres-client -- bash
```

# FICHIER CONFIG INFRA (MSD-VDM)

- chercher le fichier conf dans infra 

```bash
k get deploy -n zeus-int

// retourner la lister des pods deployer 
k get deploy -n zeus-int

// modifier le fichier manuellement 
k  edit vdm-msd-api-symfony

// modifier le fichier deployer
k  edit deploy -n zeus-int vdm-msd-api-symfony
```

 
