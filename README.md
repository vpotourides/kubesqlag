
# Installing Kubernetes On-Prem and deploying SQL Server 2019 Availability Group

## Bootstrap the cluster

The actual cluster bootstrap as described in [Creating Highly Available clusters with kubeadm](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/high-availability/) can take place.

Note that, if `${APISERVER_DEST_PORT}` has been configured to a value different from `6443` in the configuration above, `kubeadm init` needs to be told to use that port for the API Server. Assuming that in a new cluster port 8443 is used for the load-balanced API Server and a virtual IP with the DNS name `vip.mycluster.local`, an argument `--control-plane-endpoint` needs to be passed to `kubeadm` as follows:

```
# kubeadm init --control-plane-endpoint vip.mycluster.local:8443 [additional arguments ...]
```
