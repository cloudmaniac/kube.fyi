---
weight: 10
title: Upgrade Kubernetes
---

# Upgrade Kubernetes

## Perform a Version Upgrade on a Kubernetes Cluster using Kubeadm

To perform a version upgrade on a Kubernetes cluster that was installed using Kubeadm, you can use the kubeadm upgrade command. This command allows you to specify the target version that you want to upgrade to, and it will automatically handle the process of upgrading the control plane components and any necessary changes to the cluster configuration.

Here is an example of how to use the kubeadm upgrade command to upgrade a cluster to a specific version:

```
kubeadm upgrade apply --version=1.18.3
```

After running this command, the control plane components will be upgraded to version 1.18.3, and any necessary changes to the cluster configuration will be applied. Note that this process may take some time, depending on the size and complexity of your cluster.

It is important to note that this process only upgrades the control plane components of your cluster. To upgrade the versions of the Kubernetes components that are running on your worker nodes, you will need to use a different process, such as rolling upgrades or cluster-wide upgrades. For more information, you can refer to the Kubernetes documentation.

**Tainting nodes** is a feature of Kubernetes that allows you to mark certain nodes as unschedulable, preventing new workloads from being scheduled on them. This can be useful in certain situations, such as when you need to perform maintenance on a node or drain it of workloads in preparation for an upgrade.

Whether or not you should taint nodes before performing a Kubernetes upgrade will depend on your specific situation and requirements. In general, it is a good idea to drain workloads from nodes that you are planning to upgrade, to ensure that they are ready for the upgrade process. This can be done using the kubectl drain command, which will evict all of the workloads from the node and mark it as unschedulable.

If you are using the kubeadm tool to perform the upgrade, you may not need to taint the nodes beforehand, as kubeadm will automatically handle draining workloads from the nodes that are being upgraded. However, you may still want to taint the nodes as an additional precaution, to ensure that no new workloads are scheduled on them during the upgrade process.

Ultimately, the decision of whether or not to taint nodes before a Kubernetes upgrade will depend on your specific situation and requirements. You should carefully consider your options and choose the approach that is most appropriate for your situation.
