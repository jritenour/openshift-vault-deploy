# Getting started

Clone this repo, then:
1. oc new-project vault-deploy
2. docker import (image file name)
3. Get the image id of the imported image (docker images)
4. docker tag (image id) docker-registry-default.svc:5000/vault-deploy/vault-enterprise
5. docker login -u (openshfit username) -p $(oc whoami -t) docker-registry-default-svc:5000
6. docker push docker-registry.default.svc:5000/vault-deploy/vault-enterprise 
7. Edit route names in route.yaml to match your environment
8. oc create -f services.yaml
9. oc create -f serviceaccounts.yaml
10. oc create -f rolebindings.yaml
11. oc create -f configmap.yaml
12. oc adm policy add-scc-to-user privileged -n vault-deploy -z privilegeduser
13. oc create -f statefulsets.yaml
15. oc create -f routes.yaml (or ingress - see ingressexample.yaml)
16. export VAULT_ADDR=(vault route name)
18. Install vault locally
19. vault init
20. vault operator init -key-shares=1 -key-threshold=1
21. Set the unseal key as an env variable called VAULT_UNSEAL
22. vault unseal $VAULT_UNSEAL
