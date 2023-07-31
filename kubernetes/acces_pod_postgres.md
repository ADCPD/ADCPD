VDM-MSD :  

A ajouter les variable d'environnement dans (voir le cas pour SIMPLICITI): 
https://github.com/Suezenv/villagile-infra/blob/master/helm/vdm/msd-AND-waste-management/values-api.yaml

#### trouver le POD container pour vdm-msd `vdm-msd`

```bash

  kubectl -n zeus-int get po | grep dm-msd-api-symfony
  
  k -n zeus-int exec -it  vdm-msd-api-symfony-bc4f8d4fb-66l7h -- bash

```

#### trouver le POD container pour postgres `vdm-msd`

```bash
kubectl -n default get po | grep post

k -n default exec -it postgres-client  bash
```

#### connection à `vdm_msd `: 

```bash
psql -U vdm_msd@3slabdevpostgres -W -h 3slabdevpostgres.postgres.database.azure.com vdm_msd 
> password : Jlcy5wb3N0Z3Jlcy!5kYXR
```

#### connection à `waste_man `: 

```bash
psql -U waste_man@3slabdevpostgres -W -h 3slabdevpostgres.postgres.database.azure.com waste_man
> password : b3N0Z3zc2J!enVyZS5R
```

## REMOVE KILLED POD ``postgres-client``

```bash 
 k -n default delete pod postgres-client
# pod "postgres-client" deleted
```

## RELANCE KILLED POD ``postgres-client``

```bash 
kubectl -n default run --rm -it postgres-client --image=postgres /bin/bash
```


## Tester la creation d'un job : 

### Retourner la liste des `JOBS`

```bash
k get jobs
```

**msd-AND-waste-management git:(master) ✗**

```bash
k create job --from=cronjob/vdm-msd-loader-simpliciti-lift-cronjob vdm-msd-loader-simpliciti-manual
```

**Trouver le CRON creer :**

```bash
 k get po | grep simpliciti-lift
```

**Lire les logs du pods :**

```bash
k logs vdm-msd-loader-simpliciti-manual--1-czfb9
```

### verifier les JOBS lancée ( en chercher le cron par nom )

```bash
 k get jobs | grep vdm-msd-loader-simpliciti-lift
```

### verifier les POD lancée ( en chercher le cron par nom )

```bash
 k get pod | grep vdm-msd-loader-simpliciti-lift
```
