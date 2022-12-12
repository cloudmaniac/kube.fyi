---
weight: 10
title: Workloads & Scheduling
---

# Workloads & Scheduling

### Create Robust and Self-healing Application Deployments

In Kubernetes, there are several "primitives" that you can use to create robust, self-healing application deployments. These primitives are fundamental building blocks that provide the core functionality of Kubernetes, and they can be combined to create complex and powerful application deployments.

Some of the key primitives that are used to create robust, self-healing application deployments in Kubernetes are:

* **Pods**: A pod is the smallest deployable unit in Kubernetes. A pod typically contains one or more containers, and it provides a consistent environment for the containers to run in. Pods are managed by ReplicaSets, and they are the basic building blocks of applications in Kubernetes.

* **ReplicaSets**: A ReplicaSet is a deployment controller that ensures that a specified number of replicas of a pod are running at any given time. A ReplicaSet ensures that the desired number of replicas are always available, and it automatically replaces any replicas that are terminated or unavailable.

* **Deployments**: A deployment is a way to manage the lifecycle of an application or a group of related applications. A deployment defines the desired state of an application, and Kubernetes will ensure that the application is running in the desired state.

* **Services**: A service is an abstraction that defines a logical set of pods and a policy for accessing them. A service allows you to access a group of pods as if they were a single entity, and it provides load balancing, service discovery, and other features.

By using these and other primitives in Kubernetes, you can create robust, self-healing application deployments that are resilient to failures and can automatically recover from errors.

## Pods

*TBC*

## ReplicaSets

*TBC*

## Deployments

In Kubernetes, a deployment is a way to manage the lifecycle of an application or a group of related applications. A deployment defines the desired state of an application (such as the number of replicas or the container image to use), and Kubernetes will ensure that the application is running in the desired state.

A deployment in Kubernetes is represented by a Deployment resource, which is a declarative object that specifies the desired state of the application. When you create a deployment, you can specify details such as the container image to use, the number of replicas to run, and the resources (such as CPU and memory) that the application requires.

Once the deployment is created, Kubernetes will automatically manage the lifecycle of the application. This includes tasks such as rolling out new versions of the application, scaling the number of replicas up or down, and rolling back to a previous version if necessary.

Using deployments in Kubernetes can be very useful for managing the lifecycle of your applications, as it allows you to easily deploy, update, and scale your applications. For more information about deployments in Kubernetes, you can refer to the Kubernetes documentation.

To manage deployments in Kubernetes, you can use the kubectl command-line tool. The kubectl tool allows you to create, view, and delete deployments, as well as view and manage the replicas that are associated with each deployment.

Here are some examples of how you can use kubectl to manage deployments in Kubernetes:

To create a new deployment, you can use the kubectl create deployment command, followed by the necessary parameters to define the deployment. For example, to create a deployment that runs a container image named `my-image`, you could use the following command:

```
kubectl create deployment my-deployment --image=my-image
```

To view the details of a deployment, you can use the `kubectl describe deployment` command, followed by the name of the deployment. This will display information about the deployment, such as the container image and the number of replicas that are running.

To delete a deployment, you can use the `kubectl delete deployment` command, followed by the name of the deployment. This will delete the deployment, as well as any replicas that are associated with it.

To view the list of deployments in your cluster, you can use the `kubectl get deployment` command. This will display the names and details of all of the deployments in your cluster.

To perform rolling upgrades and updates with deployments in Kubernetes, you can use the kubectl command-line tool. The kubectl tool allows you to easily update the details of a deployment, such as the container image or the number of replicas, and it will automatically roll out the changes in a controlled manner.

Here are some examples of how you can use kubectl to perform rolling upgrades and updates with deployments in Kubernetes:

To update the container image of a deployment, you can use the `kubectl set image` command. For example, to update a deployment named `my-deployment` to use a new container image named `my-new-image`, you could use the following command:

```
kubectl set image deployment/my-deployment my-container=my-new-image
```

To update the number of replicas in a deployment, you can use the `kubectl scale` command. For example, to scale a deployment named `my-deployment` to have 5 replicas, you could use the following command:

```
kubectl scale deployment/my-deployment --replicas=5
```

To roll back a deployment to a previous version, you can use the `kubectl rollout undo` command. For example, to roll back a deployment named `my-deployment` to the previous version, you could use the following command:

```
kubectl rollout undo deployment/my-deployment
```

Rolling upgrades and updates with deployments in Kubernetes allows you to easily update your applications and manage their lifecycle. For more detailed information, you can refer to the Kubernetes documentation.

## ConfigMaps & Secrets

In Kubernetes, ConfigMaps and Secrets are two types of resources that you can use to configure your applications. ConfigMaps allow you to store configuration data as key-value pairs, and Secrets allow you to store sensitive data such as passwords or keys in a secure manner.

To use ConfigMaps and Secrets to configure your applications in Kubernetes, you can create the ConfigMap or Secret resource and then mount it as a volume in your application's deployment. This will allow the application to access the configuration data or secrets, and it will allow you to easily update the data without having to redeploy the application.

Here are some examples of how you can use ConfigMaps and Secrets to configure your applications in Kubernetes:

To create a ConfigMap, you can use the kubectl create configmap command. For example, to create a ConfigMap named `my-config` with two key-value pairs, you could use the following command:

```
kubectl create configmap my-config --from-literal=key1=value1 --from-literal=key2=value2
```

To create a Secret, you can use the kubectl create secret command. For example, to create a Secret named my-secret with a password and an SSH key, you could use the following command:

```
kubectl create secret generic my-secret --from-literal=password=my-password --from-file=ssh-key=my-key.pem
```

To mount a ConfigMap or Secret as a volume in your application's deployment, you can use the volumeMounts and volumes fields in the deployment's spec section. For example, to mount a ConfigMap named `my-config` and a Secret named `my-secret` in a deployment named my-deployment, you could use the following YAML:

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-deployment
spec:
  replicas: 1
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
      - name: my-container
        image: my-image
        volumeMounts:
        - name: config-volume
```

### Scale Applications

To scale an application in Kubernetes, you can use the kubectl command-line tool. The kubectl tool allows you to easily update the number of replicas in a deployment, and it will automatically roll out the changes in a controlled manner.

Here are the steps to scale an application in Kubernetes:

To view the current number of replicas in your deployment, you can use the kubectl describe deployment command, followed by the name of your deployment. For example, to view the details of a deployment named my-deployment, you could use the following command:

```
kubectl describe deployment my-deployment
```

To update the number of replicas in your deployment, you can use the kubectl scale command. For example, to scale a deployment named my-deployment to have 5 replicas, you could use the following command:

```
kubectl scale deployment/my-deployment --replicas=5
```

To view the updated number of replicas in your deployment, you can use the kubectl describe deployment command again. This will show you the new number of replicas, as well as the current status of the deployment.

Scaling an application in Kubernetes allows you to easily manage the number of replicas and the resources that are used by the application.

### Resource Limits

In Kubernetes, **resource limits** are a way to specify the maximum amount of CPU or memory that a pod is allowed to use. When resource limits are set for a pod, the Kubernetes scheduler will use this information to determine where to place the pod on the cluster.

When resource limits are set for a pod, the Kubernetes scheduler will first try to find a node that has enough available resources to satisfy the pod's limits. If the scheduler cannot find a node that has enough available resources, it will try to find a node that has available resources that are overcommitted (i.e., the node is using more resources than it has allocated to it).

If the scheduler cannot find a node that has enough available resources, even if they are overcommitted, it will not be able to schedule the pod. This means that the pod will remain in a pending state, and it will not be able to run on the cluster until a node with sufficient resources becomes available.

In general, setting resource limits for pods can help to improve the overall performance and stability of a Kubernetes cluster. It can prevent pods from using too many resources, which can cause other pods to become starved for resources and perform poorly. However, it is important to set resource limits carefully, as setting them too low can prevent pods from being scheduled on the cluster.

To manage resource limits in Kubernetes, you can use the kubectl command-line tool. The kubectl tool allows you to set resource limits for pods and other resources, and it allows you to view and manage the resource limits that are currently in place on your cluster.

Here are some examples of how you can use kubectl to manage resource limits in Kubernetes:

To set resource limits for a pod, you can use the --limits and --requests flags when creating the pod. For example, to create a pod named my-pod with a CPU limit of 1 CPU and a memory limit of 1GB, you could use the following command:

```
kubectl run my-pod --image=my-image --limits=cpu=1,memory=1Gi --requests=cpu=0.5,memory=500Mi
```

To view the resource limits that are currently set for a pod, you can use the kubectl describe pod command, followed by the name of the pod. This will display the pod's resource limits, as well as its current resource usage.

To update the resource limits for a pod, you can use the kubectl set resources command. For example, to update the CPU limit for a pod named my-pod to 2 CPUs, you could use the following command:

```
kubectl set resources pod/my-pod --limits=cpu=2
```

Managing resource limits in Kubernetes can be important for ensuring that your applications are able to run smoothly and efficiently on your cluster.

### Manifest Management

In Kubernetes, manifest management refers to the process of defining, creating, and managing the deployment and configuration of applications and other resources on a Kubernetes cluster.

Manifests in Kubernetes are written in a declarative language, such as YAML or JSON, and they specify the desired state of an application or resource. For example, a manifest might specify the container image to use, the number of replicas to run, and the resources (such as CPU and memory) that the application requires.

To manage manifests in Kubernetes, you can use the kubectl command-line tool. The kubectl tool allows you to create, view, and update manifests, and it will automatically apply the changes to the cluster to ensure that the desired state is maintained.

Manifest management in Kubernetes can be very useful for managing the deployment and configuration of your applications and other resources on a Kubernetes cluster. It allows you to easily define, create, and update your applications, and it provides a consistent and declarative way to manage the desired state of your applications.

There are several common templating tools that are used in Kubernetes to manage the deployment and configuration of applications and other resources. These tools allow you to create templates that can be used to generate manifests, and they provide a way to parameterize and customize the templates based on your specific needs.

Some of the most common templating tools that are used in Kubernetes are:

* **Helm**: Helm is a package manager for Kubernetes that allows you to manage and deploy applications on a Kubernetes cluster. Helm uses a concept called "charts" to define the structure and dependencies of an application, and it provides a templating language called Go Templating (GoTpl) for defining and customizing the templates.

* **Kustomize**: Kustomize is a tool for customizing and generating Kubernetes manifests. It allows you to create "overlays" that specify how to modify or extend an existing manifest, and it provides a templating language called HashiCorp Configuration Language (HCL) for defining and customizing the templates.

* **Ksonnet**: Ksonnet is a toolkit for developing and deploying applications on Kubernetes. It uses a concept called "components" to define the structure and dependencies of an application, and it provides a templating language called Jsonnet for defining and customizing the templates.

These templating tools can be very useful for managing the deployment and configuration of applications in Kubernetes. They provide a way to define and customize templates, and they can make it easier to manage and maintain your applications on a Kubernetes cluster.