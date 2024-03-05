# Pod Networking

  - Take me to [Lecture](https://kodekloud.com/topic/pod-networking/)

In this section, we will take a look at **Pod Networking**

Understanding Pod Networking
- Pods in Kubernetes are assigned unique IP addresses within a cluster, enabling direct communication between them. By default, each pod is isolated and has its 
  own IP address, which allows for secure communication and avoids port conflicts. These IP addresses are reachable only within the Kubernetes cluster network 
  unless specific configurations are made for external access.

Kubernetes Networking Model
- Pod-to-Pod Communication within the Same Node: When multiple pods are scheduled on the same node, they can communicate with each other directly using localhost 
  or the loopback interface. This communication happens through the pod’s assigned IP address within the cluster, typically in the form of a Virtual Ethernet 
  (veth) pair. The communication occurs at the network layer, enabling high-performance and low-latency interactions between pods on the same node.
  
-  Pod-to-Pod Communication across Nodes: When pods need to communicate across different nodes in the cluster, Kubernetes employs various networking solutions, 
  such as Container Network Interfaces (CNIs) and software-defined networking (SDN) technologies. These solutions create a virtual network overlay that spans the 
  entire cluster, enabling pod-to-pod communication across nodes. Some popular CNIs include Calico, Flannel, Weave, and Cilium. These networking solutions ensure 
  that the pod’s IP address remains reachable and provides transparent network connectivity regardless of the pod’s location within the cluster.

Cluster-Internal Communication
- By default, pods within a Kubernetes cluster can communicate with each other using their internal IP addresses. This communication happens over a virtual network overlay provided by the underlying container runtime or network plugin. The internal IP addresses are assigned by the Kubernetes cluster networking solution and are routable only within the cluster.

DNS-Based Service Discovery
- Kubernetes provides a built-in DNS service for service discovery within the cluster. Services act as stable endpoints that abstract the underlying pods. Each service is assigned a DNS name, which resolves to the IP addresses of the pods backing that service. This DNS-based approach allows pods to communicate with each other using the service names rather than directly referencing the individual pod IP addresses.

Service Load Balancing
- When multiple pods are serving the same application, Kubernetes provides built-in load balancing capabilities for distributing traffic across those pods. By creating a service object and associating it with a set of pods, Kubernetes automatically load balances the incoming requests among the available pods. This load balancing mechanism ensures high availability and scalability of the application.

Network Policies
- Kubernetes offers network policies as a means to control traffic flow between pods. Network policies define rules that specify which pods can communicate with each other based on various parameters such as IP addresses, ports, and protocols. By enforcing network policies, you can segment your application’s network traffic and add an additional layer of security.

External Communication
- Pods often need to communicate with resources outside the Kubernetes cluster, such as external services or databases. Kubernetes provides several mechanisms to facilitate this external communication. One approach is to expose a pod or a set of pods using a service of type “LoadBalancer” or “NodePort,” allowing external clients to access the pods. Another option is to use an Ingress controller, which provides a way to route incoming traffic from outside the cluster to the appropriate pods based on defined rules.

Service Mesh
- For advanced networking scenarios, a service mesh can be employed to enhance pod-to-pod communication. A service mesh, such as Istio or Linkerd, sits as a layer on top of the Kubernetes cluster and provides features like traffic management, observability, and security. With a service mesh, you can control and monitor the communication between pods with advanced routing rules, circuit breaking, and distributed tracing.


- To add bridge network on each node

> node01
```
$ ip link add v-net-0 type bridge
```
> node02
```
$ ip link add v-net-0 type bridge
```

> node03
```
$ ip link add v-net-0 type bridge
```

- Currently it's down, turn it up.

> node01
```
$ ip link set dev v-net-0 up
```

> node02
```
$ ip link set dev v-net-0 up
```

> node03
```
$ ip link set dev v-net-0 up
```

- Set the IP Addr for the bridge interface

> node01
```
$ ip addr add 10.244.1.1/24 dev v-net-0
```

> node02
```
$ ip addr add 10.244.2.1/24 dev v-net-0
```

> node03
```
$ ip addr add 10.244.3.1/24 dev v-net-0
```

![net-11](../../images/net11.PNG)

- Check the reachability 

```
$ ping 10.244.2.2
Connect: Network is unreachable
```

- Add route in the routing table
```
$ ip route add 10.244.2.2 via 192.168.1.12
```

> node01
```
$ ip route add 10.244.2.2 via 192.168.1.12

$ ip route add 10.244.3.2 via 192.168.1.13
```

> node02
```
$ ip route add 10.244.1.2 via 192.168.1.11

$ ip route add 10.244.3.2 via 192.168.1.13

```

> node03
```
$ ip route add 10.244.1.2 via 192.168.1.11

$ ip route add 10.244.2.2 via 192.168.1.12
```

- Add a single large network 

![net-12](../../images/net12.PNG)


## Container Network Interface

![net-13](../../images/net13.PNG)






#### References Docs

- https://kubernetes.io/docs/concepts/workloads/pods/
