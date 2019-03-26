# Getting started

1. Clone this repo
2. Edit route names in route.yaml to match your environment
3. oc create -f serviceaccounts.yaml
4. oc create -f rolebindings.yaml
5. oc create -f endpoints.yaml
6. oc create -f configmap.yaml
7. oc create -f statefulsets.yaml
8. oc create -f routes.yaml
9. export VAULT_ADDR=(vault route name)
10. Install vault locally
11. vault init
12. vault operator init -key-shares=1 -key-threshold=1
13. Set the unseal key as an env variable called VAULT_UNSEAL
14. vault unseal $UNSEAL_KEY
