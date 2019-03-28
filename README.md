# Getting started

1. Clone this repo
2. Edit route names in route.yaml to match your environment
3. oc create -f services.yaml
4. oc create -f serviceaccounts.yaml
5. oc create -f rolebindings.yaml
6. oc create -f endpoints.yaml
7. oc create -f configmap.yaml
8. oc create -f statefulsets.yaml
9. oc create -f routes.yaml (or ingress - see ingressexample.yaml)
10. export VAULT_ADDR=(vault route name)
11. Install vault locally
12. vault init
13. vault operator init -key-shares=1 -key-threshold=1
14. Set the unseal key as an env variable called VAULT_UNSEAL
15. vault unseal $UNSEAL_KEY
