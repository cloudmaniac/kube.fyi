---
weight: 10
title: RBAC
---

# Kubernetes Role-Based Access Control

**RBAC**, or **Role-Based Access Control**, is a feature of Kubernetes that allows you to control access to resources in your cluster. With RBAC, you can specify which users or service accounts have access to which resources, and what actions they are allowed to perform on those resources. This allows you to ensure that only authorized users have access to your cluster and its resources, and that they can only perform the actions that you have granted them permission to do.

To manage RBAC in Kubernetes, you can use the kubectl command-line tool. The kubectl tool allows you to create and manage roles and role bindings, which define the permissions that users or service accounts have in your cluster.

Here are some examples of how you can use kubectl to manage RBAC in Kubernetes:

To create a role that allows a user to list, get, and watch deployments in a specific namespace, you can use the following command:

```
kubectl create role deployment-manager --verb=list,get,watch --resource=deployments --namespace=mynamespace
```

To grant a user access to the role you just created, you can use the kubectl create rolebinding command, like this:

```
kubectl create rolebinding deployment-manager-binding --role=deployment-manager --user=user1
```

To view the roles and role bindings that have been created in your cluster, you can use the `kubectl get roles` and `kubectl get rolebindings` commands, respectively.

To delete a role or role binding, you can use the `kubectl delete role` and `kubectl delete rolebinding` commands, followed by the name of the role or role binding you want to delete.
