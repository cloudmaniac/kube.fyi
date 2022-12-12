---
weight: 20
title: Services & Networking
---

# Services & Networking in Kubernetes

## Cluster Nodes Host Networking Configuration

In Kubernetes, the host networking configuration on the cluster nodes defines how the network is set up and how the containers on the nodes are able to communicate with each other and with external networks.

When a Kubernetes cluster is created, the nodes in the cluster are typically connected to a network using a network plugin, such as the Kubernetes network plugin (kubenet) or a third-party plugin. The network plugin is responsible for providing network connectivity to the nodes, and it defines how the containers on the nodes are able to communicate with each other and with external networks.

The host networking configuration on the cluster nodes can be managed using the kubectl command-line tool. The kubectl tool allows you to view and modify the network configuration for the nodes in the cluster, and it provides commands for managing the network plugin and other networking components.

Understanding the host networking configuration on the cluster nodes in Kubernetes can be important for managing the network connectivity and communication between containers on the nodes.

## Pod Connectivity

In Kubernetes, connectivity between pods works by using the network plugin that is configured on the cluster. The network plugin is responsible for providing network connectivity to the pods, and it defines how the pods are able to communicate with each other and with external networks.

When a pod is created in Kubernetes, it is automatically assigned an IP address by the network plugin. The IP address is unique to the pod, and it is used to identify the pod on the network.

To enable connectivity between pods, the network plugin uses a combination of network interfaces, IP addresses, and routing rules to forward traffic between the pods. For example, when a pod sends traffic to another pod, the network plugin will use the destination pod's IP address to determine where to route the traffic, and it will forward the traffic to the destination pod using the appropriate network interface.

In general, the connectivity between pods in Kubernetes is transparent to the applications running in the pods, and the applications can communicate with each other using the standard network protocols (such as TCP and UDP).

### Service Types & Endpoints

In Kubernetes, there are several service types that you can use to expose your applications to external networks. These service types define different ways of exposing the applications, and they provide different levels of access and functionality.

The three most common service types in Kubernetes are:

* **ClusterIP**: A ClusterIP service is a service that is only accessible within the cluster. It exposes the application on a cluster-internal IP address, and it is not accessible from outside of the cluster.

* **NodePort**: A NodePort service is a service that exposes the application on a specific port on each node in the cluster. This allows the application to be accessed from outside of the cluster by accessing the nodes using their IP addresses and the specified port.

* **LoadBalancer**: A LoadBalancer service is a service that exposes the application using a load balancer. The load balancer is typically provided by a cloud provider, and it distributes incoming traffic across the nodes in the cluster. This allows the application to be accessed from outside of the cluster using a single, external IP address.

In addition to these service types, Kubernetes also provides a concept called "endpoints" that allows you to specify the target pods for a service. An endpoint is a logical entity that represents the network addressable endpoints for a service, and it allows you to control which pods are included in the service.

For example, if you have a deployment with 10 replicas of a pod, you can create an endpoint that includes only 5 of the replicas, and you can create a service that uses the endpoint to expose only the 5 selected replicas. This allows you to fine-tune the behavior of the service, and it provides more flexibility and control over how the service is exposed.

In general, the ClusterIP, NodePort, and LoadBalancer service types provide different ways of exposing your applications in Kubernetes, and endpoints allow you to control which pods are included in the service.

To manage services in Kubernetes, you can use the kubectl command-line tool. The kubectl tool allows you to create, view, and update services, and it provides commands for managing the different service types and endpoints.

Here are some examples of how you can use kubectl to manage services in Kubernetes:

To create a new service, you can use the `kubectl create service` command. For example, to create a ClusterIP service named my-service that exposes a deployment named my-deployment, you could use the following command:

```
kubectl create service clusterip my-service --targets=my-deployment
```

To view the details of a service, you can use the `kubectl describe service` command, followed by the name of the service. This will display information about the service, such as its type, endpoints, and associated pods.

To update an existing service, you can use the `kubectl edit service` command, followed by the name of the service. This will open the service's manifest in an editor, and you can make the desired changes and save the file to apply the changes to the service.

### Ingress Controllers & Ingress Resources

In Kubernetes, Ingress controllers and Ingress resources are used to manage external access to the applications on a Kubernetes cluster. An Ingress controller is a load balancer that is responsible for routing incoming traffic to the appropriate services, and an Ingress resource is a Kubernetes resource that defines the rules for routing the traffic.

To use Ingress controllers and Ingress resources in Kubernetes, you need to do the following:

1. Install an Ingress controller on your cluster. An Ingress controller is a piece of software that runs on your cluster and manages the incoming traffic. There are several different Ingress controllers that you can use, such as NGINX or HAProxy, and you can choose the one that best fits your needs.

2. Create Ingress resources to define the rules for routing the incoming traffic. An Ingress resource is a Kubernetes resource that defines how the incoming traffic should be routed to the services on your cluster. It specifies the hostname and path that should be used to route the traffic, and it defines the service that should receive the traffic.

3. Update your services to use the Ingress resources. When you create an Ingress resource, you need to specify the service that should receive the incoming traffic. To do this, you need to update your services to use the Ingress resource as their endpoint, and you need to specify the hostname and path that should be used to route the traffic to the service.

Using Ingress controllers and Ingress resources in Kubernetes can provide several benefits, such as improved security, better performance, and easier management of external access to your applications.

An Ingress resource is a Kubernetes resource that defines the rules for routing incoming traffic to the services on a Kubernetes cluster. Here is an example of an Ingress resource that routes incoming traffic for the hostname `www.example.com` to a service named `my-service`:

```
apiVersion: networking.k8s.io/v1beta1
kind: Ingress
metadata:
  name: my-ingress
spec:
  rules:
  - host: www.example.com
    http:
      paths:
      - path: /
        backend:
          serviceName: my-service
          servicePort: 80
```

This Ingress resource specifies that incoming traffic for the hostname `www.example.com` should be routed to the service my-service on port 80. The traffic is routed using the `/` path, which means that all traffic for `www.example.com` will be routed to the service.

You can customize the Ingress resource by adding additional rules, paths, and backends to route the traffic to different services based on the hostname, path, or other criteria. For more detailed information, you can refer to the Kubernetes documentation.

### Container Network Interface

In Kubernetes, a container network interface (CNI) plugin is a piece of software that is responsible for providing network connectivity to the containers on a Kubernetes cluster. There are several different CNI plugins that you can choose from, and each one has its own strengths and limitations.

To choose an appropriate CNI plugin for your Kubernetes cluster, you need to consider several factors, such as the following:

The type of network connectivity that you need: Different CNI plugins provide different types of network connectivity, such as overlay networks, VLANs, or VXLANs. You need to choose a CNI plugin that provides the type of connectivity that you need for your applications.

The performance and scalability requirements of your applications: Some CNI plugins are better suited for high-performance and scalable environments, while others are more suited for smaller, simpler deployments. You need to choose a CNI plugin that can meet the performance and scalability requirements of your applications.

The level of customization and flexibility that you need: Some CNI plugins are highly customizable and allow you to fine-tune the network configuration, while others are more opinionated and provide less flexibility. You need to choose a CNI plugin that provides the level of customization and flexibility that you need for your deployment.

The compatibility with other components and tools: You need to choose a CNI plugin that is compatible with the other components and tools that you are using in your Kubernetes deployment. This includes the Kubernetes version, the network and storage plugins, and the other tools and frameworks that you are using.

Choosing the right CNI plugin for your Kubernetes cluster is an important decision, and it can have a significant impact on the performance, reliability, and scalability of your applications.

### CoreDNS

CoreDNS is a DNS server that is used to provide DNS services in Kubernetes. It is a pluggable, extendable, and customizable DNS server that can be used to provide DNS services for the applications on a Kubernetes cluster. Using CoreDNS in Kubernetes can provide several benefits, such as improved performance, better reliability, and more flexibility and customization.

To configure and use CoreDNS in Kubernetes, you need to do the following:

1. Install CoreDNS on your Kubernetes cluster. CoreDNS can be installed using the Kubernetes package manager, Helm, or by using the Kubernetes manifests directly.

2. Configure CoreDNS to use the appropriate upstream DNS servers. CoreDNS needs to be configured to use the appropriate upstream DNS servers to resolve DNS queries for the applications on your cluster. This can be done by editing the CoreDNS configuration file and specifying the upstream servers.

3. Update the Kubernetes DNS service to use CoreDNS. In Kubernetes, the DNS service is responsible for providing DNS services to the applications on the cluster. By default, Kubernetes uses the kube-dns service for DNS, but you can update it to use CoreDNS instead. This can be done by modifying the Kubernetes DNS service configuration.

4. Use CoreDNS to resolve DNS queries for the applications on your cluster. Once CoreDNS is installed and configured, you can use it to resolve DNS queries for the applications on your cluster. This can be done using the standard DNS protocols and tools, such as nslookup or dig.
