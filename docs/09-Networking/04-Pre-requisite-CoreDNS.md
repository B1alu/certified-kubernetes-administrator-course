# Pre-requisite CoreDNS

  - Take me to [Lecture](https://kodekloud.com/topic/prerequisite-coredns/)

In this section, we will take a look at **CoreDNS**
- CoreDNS is an important component of Kubernetes because it provides a reliable and scalable way to perform DNS-based service discovery and name resolution within a Kubernetes cluster. This is essential for enabling communication between pods and services in a complex and dynamic containerized environment.
- CoreDNS is deployed in a simple way: It runs as a cluster-level Pod and handles DNS queries within the cluster from there. By default, the service is named kube-dns.
- The CoreDNS server is deployed as a POD in the kube-system namespace in the Kubernetes cluster. Well they are deployed as two pods for redundancy, as part of a ReplicaSet. They are actually a replicaset within a deployment.
  
- Kubernetes relies on the Domain Name System (DNS) to enable seamless communication between its various components, such as pods and services.
- When a new Kubernetes service is created, the platform automatically generates a DNS record for it, allowing other pods to easily locate and connect to the service. Kubernetes also offers support for ExternalDNS, which simplifies the process of creating and managing DNS records for services that need to be accessible externally. This makes it easier for external clients to access the services within the cluster.
- Kubernetes uses DNS to help pods and services find and communicate with each other using hostnames.
- When a Kubernetes service is created, a DNS record is automatically generated for it.

## Installation of CoreDNS

```
$ wget https://github.com/coredns/coredns/releases/download/v1.7.0/coredns_1.7.0_linux_amd64.tgz
coredns_1.7.0_linux_amd64.tgz

```

## Extract tar file

```
$ tar -xzvf coredns_1.7.0_linux_amd64.tgz
coredns
```

## Run the executable file

- Run the executable file to start a DNS server. By default, it's listen on port 53, which is the default port for a DNS server.

```
$ ./coredns

```

## Configuring the hosts file

- Adding entries into the `/etc/hosts` file.
- CoreDNS will pick the ips and names from the `/etc/hosts` file on the server.

```
$ cat > /etc/hosts
192.168.1.10    web
192.168.1.11    db
192.168.1.15    web-1
192.168.1.16    db-1
192.168.1.21    web-2
192.168.1.22    db-2
```

## Adding into the Corefile

```
$ cat > Corefile
. {
	hosts   /etc/hosts
}

```

## Run the executable file

```
$ ./coredns

```


#### References Docs

- https://github.com/kubernetes/dns/blob/master/docs/specification.md
- https://coredns.io/plugins/kubernetes/
- https://github.com/coredns/coredns/releases
