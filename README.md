
# Installing Kubernetes On-Prem and deploying SQL Server 2019 Availability Group

## Bootstrap the cluster

The actual cluster bootstrap as described in [Creating Highly Available clusters with kubeadm](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/high-availability/) can take place.
Assuming that in a new cluster a virtual IP with the DNS name `vip.mycluster.local`, an argument `--control-plane-endpoint` needs to be passed to `kubeadm` as follows:
```
# kubeadm init --control-plane-endpoint vip.mycluster.local [additional arguments ...]
```

Note that, if `${APISERVER_DEST_PORT}` has been configured to a value different from `6443` in the configuration above, `kubeadm init` needs to be told to use that port for the API Server. Assuming that in a new cluster port 8443 is used for the load-balanced API Server and a virtual IP with the DNS name `vip.mycluster.local`, an argument `--control-plane-endpoint` needs to be passed to `kubeadm` as follows:

```
# kubeadm init --control-plane-endpoint vip.mycluster.local:8443 [additional arguments ...]
```

##Highly available Kubernetes cluster using kubeadm

In my case I chose to setting up a highly available Kubernetes cluster using kubeadm,  with stacked control plane nodes. This approach requires less infrastructure. The etcd members and control plane nodes are co-located. With stacked control plane nodes. This approach requires less infrastructure. The etcd members and control plane nodes are co-located. 
For providing load balancing from a virtual IP the combination keepalived and haproxy has been around for a long time and can be considered well-known and well-tested.
This combination can be run as services on the operating system.


## Configure Highly Available HAProxy with Keepalived on Ubuntu 20.04

To configure a high-availability cluster on the Ubuntu 20.04 virtual machine, I use the description of the steps from [here](https://kifarunix.com/configure-highly-available-haproxy-with-keepalived-on-ubuntu-20-04/) and from [here](https://github.com/kubernetes/kubeadm/blob/master/docs/ha-considerations.md#bootstrap-the-cluster).

