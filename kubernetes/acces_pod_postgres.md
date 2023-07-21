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
