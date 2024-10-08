### Credits
This is a minimal version of Will's TMC Multitenant example @ https://github.com/warroyo/flux-tmc-multitenant 

We're also borrowed some of the Prometheus bits from Rick @ https://github.com/rroque99/tmc-poc

### Summary

When you create a clustergroup, point TMC at the corresponding `clustergroups/<cluster_group>` folder.

This will create two major Kustomizations on each cluster in the group

1. It will leverage secretgen-controller to copy the name of the cluster to a secret in the ` tanzu-continuousdelivery-resources` namespace
2. It then uses that cluster name as a variable to point a Kustomization at `cluster/<clustername>`

In this case, `pines-homelab-dev` and `pines-homelab-qa` are both configured to deploy the prometheus community stack, but in dev we will expose grafana via a LoadBalancer.