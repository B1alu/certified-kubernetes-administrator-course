# Pre-requisite CNI

  - Take me to [Lecture](https://kodekloud.com/topic/prerequsite-cni/)

In this section, we will take a look at **Pre-requisite Container Network Interface(CNI)**

- Kubernetes 1.29 supports Container Network Interface (CNI) plugins for cluster networking.
- A CNI plugin is required to implement the Kubernetes network model.
- Installation
A Container Runtime, in the networking context, is a daemon on a node configured to provide CRI Services for kubelet. In particular, the Container Runtime must be configured to load the CNI plugins required to implement the Kubernetes network model


![net-7](../../images/net7.PNG)

## Third Party Network Plugin Providers

- [Weave](https://www.weave.works/docs/net/latest/kubernetes/kube-addon/#-installation)
- [Calico](https://docs.projectcalico.org/getting-started/kubernetes/quickstart)
- [Flannel](https://github.com/coreos/flannel/blob/master/Documentation/kubernetes.md)
- [Cilium](https://github.com/cilium/cilium)


## To view the CNI Network Plugins

- CNI comes with the set of supported network plugins. 

```
$ ls /opt/cni/bin/
bridge  dhcp  flannel  host-device  host-local  ipvlan  loopback  macvlan  portmap  ptp  sample  tuning  vlan
```




#### References Docs

- https://kubernetes.io/docs/concepts/extend-kubernetes/compute-storage-net/network-plugins/


