# Redis-shake-AKS
### This project is used to deploy Redis-shake in aks with helm charts

step1: fetch the soure code

```
git clone  git@github.com:fudanzz/redis-shake-aks.git
```

step2: update the value.yaml to match your Redis cluster configuration

step3: package as helm charts
```
cd redis-shake-aks
helm package .
```

step4: push into ACR

before push, you should create the registry first and login, detailed steps can be found in https://docs.microsoft.com/en-us/azure/container-registry/container-registry-helm-repos

```
helm push redis-shake-0.15.1.tgz oci://$ACR_NAME.azurecr.cn/helm
az acr repository show --name $ACR_NAME --repository helm/redis-shake
```

step5: deploy into AKS

```
helm install main oci://$ACR_NAME.azurecr.cn/helm/redis-shake

helm list
```

step6: you can use helm uninstall to delete the deployment
```
helm list
helm uninstall xxxx
```