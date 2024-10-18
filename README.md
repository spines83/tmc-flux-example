(Warning: This is on a branch and these docs need to be updated accordingly) 

### Credits
This is a minimal version of Will's TMC Multitenant example @ https://github.com/warroyo/flux-tmc-multitenant -- check it out for a more production-like example

We also borrowed some of the Prometheus bits from Rick @ https://github.com/rroque99/tmc-poc

### Summary

When you create a clustergroup, point TMC at the corresponding `clustergroups/<cluster_group>` folder.

This will create two Kustomizations on each cluster in the group

1. It will leverage secretgen-controller to copy the name of the cluster to a secret in the ` tanzu-continuousdelivery-resources` namespace
2. It then uses that cluster name as a variable to point a Kustomization at `cluster/<clustername>`

In this case, `pines-homelab-dev` and `pines-homelab-qa` are both configured to deploy the prometheus community stack, but in dev we will expose grafana via a LoadBalancer.

### Deploying to TMC

#### Add your GitRepository

Navigate to Cluster Groups > (Your cluster group) > Add-Ons > Sources > Git Repositories

Add a Git Repository with the following
* Name = infra-gitops
* Repository URL = https://github.com/spines83/tmc-flux-example.git
* Repository Credential = (No Credentials Needed)
* Advanced Settings/Branch = Main

(Update the above with your repository info, if you change the name from `infra-gitops`, update the refs in the associated flux objects)

#### Deploy the root Kustomization

Navigate to Cluster Groups > (Your cluster group) > Add-Ons > Continuous Delivery > Installed Kustomizations

Add a Kustomization with the following
* Name = clustergroup
* Repository = infra-gitops
* Path = /clustergroups/pines-homelab
* (Optional) Advanced Settings/Prune = Enabled