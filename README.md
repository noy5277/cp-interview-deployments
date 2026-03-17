# cp-interview-deployments
cp-interview-deployments

## argocd initial secret
```
 kubectl -n argocd get secret argocd-initial-admin-secret   -o jsonpath="{.data.password}" | base64 -d
```