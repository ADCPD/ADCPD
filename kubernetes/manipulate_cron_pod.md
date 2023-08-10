
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

### CREATE CRON JON 

```bash
kubectl create job vdm-msd-loader-simpliciti-lift-cronjob --from cronjob/vdm-msd-loader-simpliciti-lift-cronjob --dry-run=client -o json | jq '.spec.template.spec.containers[0] += { command:["tail","-f","/dev/null"] }' | kubectl create -f -
```

- ACCESS ON BASH TO CRON JOB

```bash
kubectl -n zeus-int exec -it vdm-msd-loader-simpliciti-lift-cronjob--1-b4zsc /bin/bash
```

- Show logs

```bash
  kubectl -n zeus-int logs vdm-msd-loader-simpliciti-lift-cronjob-28191525--1-s22bl
```
