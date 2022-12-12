---
weight: 1
title: Kubernetes Concepts
---

# Kubernetes Concepts

## Architecture

Kubernetes is a popular open-source system for automating the deployment, scaling, and management of containerized applications.

It provides a platform for creating and managing clusters of containerized applications, allowing developers to focus on building their applications rather than the underlying infrastructure.

Kubernetes uses a declarative approach to cluster management, allowing users to specify the desired state of their applications and the system takes care of ensuring that the actual state matches the desired state. This makes it easier to deploy and manage complex applications at scale.

Kubernetes has a modular architecture that consists of a number of different components that work together to provide the core functionality of the system. The main components of a Kubernetes cluster include:

* The **API server**, which is the central control plane for the cluster and provides the API for managing and configuring the cluster.
* The **etcd distributed key-value store**, which is used to store the cluster's data and configuration.
* The **scheduler**, which is responsible for scheduling containers to run on the cluster's nodes.
* The **kubelet**, which is a process that runs on each node and is responsible for managing the containers running on that node.
* The **kube-proxy**, which is a network proxy that runs on each node and is responsible for implementing the network routing rules for the containers running on that node.
* The **container runtime**, which is responsible for running the containers on each node.

These components work together to provide the core functionality of Kubernetes, including deployment, scaling, and management of containerized applications. Additionally, there are other components that provide additional features and functionality, such as the Kubernetes dashboard, which provides a web-based interface for managing the cluster, and the kubectl command-line tool, which provides a command-line interface for interacting with the cluster.

## ETCD

*TBC*
