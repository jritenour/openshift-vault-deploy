# Getting started

Clone this repo, then:
1. oc new-project vault-deploy
2. Edit route names in route.yaml to match your environment
3. oc create -f services.yaml
4. oc create -f serviceaccounts.yaml
5. oc create -f rolebindings.yaml
6. oc create -f endpoints.yaml
7. oc create -f configmap.yaml
8. oc adm policy add-scc-to-user privileged -n vault-deploy -z privilegeduser
9. oc create -f statefulsets.yaml
10. oc create -f routes.yaml (or ingress - see ingressexample.yaml)
11. export VAULT_ADDR=(vault route name)
12. Install vault locally
13. vault init
14. vault operator init -key-shares=1 -key-threshold=1
15. Set the unseal key as an env variable called VAULT_UNSEAL
16. vault unseal $VAULT_UNSEAL
