# Deploy HashiCorp Vault (and Consul) on OpenShift

This will deploy Vault & Consul on OpenShift (tested on 3.10 & 3.11).  Vault will use Consul as a storage backend, and Consul will manage the Vault Cluster.

As configured, this will deploy the open source images of each from Docker hub, but you can supply your own enterprise image by either building & pushing to OpenShift's registry (outlined in steps 2-6), or by using another registry OpenShift is configured to pull from. 

Note, this is configured to deploy single replicas of each.  If you plan to deploy more pods, then update the "replicas" count in the statefulset files, and addition retry-join statements under the startup args for the containers in the stateful set.  For ingressexample

######           - -retry-join=consul-0.consul.$(NAMESPACE).svc.cluster.local
######           - -retry-join=consul-1.consul.$(NAMESPACE).svc.cluster.local

######           - -retry-join=consul-2.consul.$(NAMESPACE).svc.cluster.local

To get started,

Clone this repo, then:
1. oc new-project vault-deploy
#### If deploying Consul + Vault Enterprise, follow steps 2-6, otherwise skip to step 7.
2. docker import (image file name)
3. Get the image id of the imported images for Consul/Vault (docker images)
4. docker tag (image id) docker-registry-default.svc:5000/vault-deploy/*product*-enterprise
5. docker login -u (openshfit username) -p $(oc whoami -t) docker-registry-default-svc:5000
6. docker push docker-registry.default.svc:5000/vault-deploy/*product*-enterprise
7. Edit route names in route.yaml to match your environment
8. oc create -f consul-service.yaml
9. oc create -f vault-service.yaml
10. oc create -f configmap.yaml
11. oc create serviceaccount -n vault-deploy privilegeduser
12. oc adm policy add-scc-to-user privileged -n vault-deploy -z privilegeduser
13. oc create -f consul-statefulsets.yaml
14. oc create -f vault-statefulsets.yaml
15. oc create -f routes.yaml (or ingress - see ingressexample.yaml)
16. export VAULT_ADDR=(vault route name with http/https prefix)
17. Install vault binary locally
18. vault operator init -key-shares=1 -key-threshold=1
19. Set the unseal key as an env variable called VAULT_UNSEAL
20. vault operator unseal $VAULT_UNSEAL
