# VDM-MSD 

## Project Waste-management : Compteur exploitant

#### Repository :
```
https://github.com/Suezenv/vdm-msd
```

#### SWAGGER API :
```text
# Local API :
http://localhost:4020/api/doc/waste_management

# INT API :
https://api-msd.int.villagile.fr/api/doc/waste_management
```


Branch initial pour le developpement : `dev`

Une fois le developpement est ralisée pusher votre code sur la branch `DEV` et lancer a partir de la racine du projet :

```bash
sh create-release.sh
```
à suivre le deployement sur `Jenkins` : https://jenkins.k8s-dev.3slab.io/job/vdm-msd/
si la pipeline (release ne se charge pas ...), lancer manuellement la fetch des release en cours ... 

![image](https://github.com/ADCPD/ADCPD/assets/10563431/a94ee3b7-3e89-45cc-9f9f-fce1590a413c)

#### CRON:
> Apres chaque mise à jour de `release` penser a mettre à jour le CRON SIMPLICITI dans https://github.com/Suezenv/villagile-infra/tree/master/helm/vdm/msd-AND-waste-management/simpliciti-lift-collector-import-cronjob

```bash
cd ./villagile-infra/helm/vdm/msd-AND-waste-management
```

Exporter les variables d'environnement selon votre environnement de deploiement :

```bash
export HELM_VERSION=helm
export ENV=int
export NAMESPACE=zeus-int

export HELM_VERSION=helm
export NAMESPACE=default
export ENV=preprod

export HELM_VERSION=helm
export NAMESPACE=default
export ENV=prod
```

```bash
# Verifier la verison de tag à deployer
 
export IMAGE_TAG=$(kubectl --namespace=${NAMESPACE} get deployment vdm-msd-api-symfony -o jsonpath='{.spec.template.spec.containers[0].image}' | cut -d':' -f 2)
echo "Version : ${IMAGE_TAG}"

# Ensuite upgrade existant CRON

$HELM_VERSION upgrade --namespace=$NAMESPACE vdm-msd-loader-simpliciti-lift  3slab/cronjob -f simpliciti-lift-collector-import-cronjob/values.yaml --version=1.3.0  --set image.tag=$IMAGE_TAG --debug --dry-run

# Si le CRON n'existe pas

$HELM_VERSION install --namespace=$NAMESPACE vdm-msd-loader-simpliciti-lift  3slab/cronjob -f simpliciti-lift-collector-import-cronjob/values.yaml --version=1.3.0  --set image.tag=$IMAGE_TAG --debug --dry-run

```
Remove `--dry-run` and `--debug` when result is satisfying


