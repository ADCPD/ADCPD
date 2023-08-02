# JENKINS

#### Find conf ingress

```bash
 k -n  cicd get ingress
```
 
#### Find pod jenkins

```bash
 k -n  cicd get pod
```

#### Kill POD Jenkins & Reload

```bash
 k -n cicd delete pod cicd-jenkins-0
```
