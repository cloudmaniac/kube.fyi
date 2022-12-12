---
weight: 30
title: Storage
---

# Working with Storage in Kubernetes

## Storage Classes

In Kubernetes, a **storage class** is a way to dynamically provision storage for your applications. It allows you to specify the type and configuration of the storage that you want to use, and Kubernetes will automatically create and manage the storage for you.

A storage class is defined by a set of parameters, such as the type of storage (e.g. local disk, network-attached storage, cloud-based storage), the performance characteristics (e.g. IOPS, throughput), and the availability and durability guarantees. When you create a persistent volume claim (PVC) in Kubernetes, you can specify the storage class that you want to use, and Kubernetes will create a volume that matches the parameters of the storage class.

Using storage classes can be very useful for managing the storage needs of your applications, as it allows you to easily provision and manage storage without having to manually configure and manage individual storage volumes. It also allows you to use different types of storage for different applications or workloads, depending on their specific requirements.

To manage storage classes in Kubernetes, you can use the kubectl command-line tool. The kubectl tool allows you to create, view, and delete storage classes, as well as view the persistent volumes (PVs) and persistent volume claims (PVCs) that are associated with each storage class.

Here are some examples of how you can use kubectl to manage storage classes in Kubernetes:

To create a new storage class, you can use the `kubectl create storageclass` command, followed by the necessary parameters to define the storage class. For example, to create a storage class that uses local disk storage and has a performance of 100 IOPS, you could use the following command:

```
kubectl create storageclass my-storage-class --provisioner=kubernetes.io/no-provisioner --volume-binding-mode=WaitForFirstConsumer --parameters='{"type":"local","performance":"100"}'
```

To view the details of a storage class, you can use the `kubectl describe storageclass` command, followed by the name of the storage class. This will display information about the storage class, such as its parameters and the PVs and PVCs that are associated with it.

To delete a storage class, you can use the `kubectl delete storageclass` command, followed by the name of the storage class. This will delete the storage class, as well as any PVs and PVCs that are associated with it.

To view the list of storage classes in your cluster, you can use the `kubectl get storageclass` command. This will display the names and details of all of the storage classes in your cluster.

Managing storage classes in Kubernetes can be complex, and it requires careful planning and configuration. For more detailed information, you can refer to the Kubernetes documentation.

## Persistent Volumes

In Kubernetes, a **persistent volume (PV)** is a piece of storage that is abstracted from the underlying infrastructure, and can be easily consumed by applications. PVs are typically backed by some type of storage infrastructure, such as local disks, network-attached storage, or cloud-based storage.

PVs are designed to be long-lived, and they can be used by multiple applications or workloads within a Kubernetes cluster. When an application needs to use storage, it can request a persistent volume claim (PVC), which will cause Kubernetes to dynamically provision a PV that matches the PVC's requirements. The PV can then be mounted by the application, allowing it to access the storage.

Using PVs and PVCs in Kubernetes allows you to easily manage and consume storage within your applications. It allows you to abstract the details of the underlying storage infrastructure, and it allows you to easily scale and manage the storage needs of your applications.

To manage persistent volumes (PVs) in Kubernetes, you can use the kubectl command-line tool. The kubectl tool allows you to create, view, and delete PVs, as well as view the persistent volume claims (PVCs) that are associated with each PV.

Here are some examples of how you can use kubectl to manage PVs in Kubernetes:

To create a new PV, you can use the `kubectl create pv` command, followed by the necessary parameters to define the PV. For example, to create a PV that uses a local disk and has a capacity of 10GB, you could use the following command:

```
kubectl create pv my-pv --capacity=10Gi --access-modes=ReadWriteOnce --storage-class=my-storage-class --hostpath= /mnt/my-disk
```

To view the details of a PV, you can use the `kubectl describe pv` command, followed by the name of the PV. This will display information about the PV, such as its capacity, access modes, and the PVCs that are associated with it.

To delete a PV, you can use the `kubectl delete pv` command, followed by the name of the PV. This will delete the PV, as well as any PVCs that are associated with it.

To view the list of PVs in your cluster, you can use the kubectl get pv command.

To manage volumes in Kubernetes, you can use the kubectl command-line tool. The kubectl tool allows you to create, view, and delete volumes, as well as view the persistent volume claims (PVCs) that are associated with each volume.

Here are some examples of how you can use kubectl to manage volumes in Kubernetes:

To create a new volume, you can use the `kubectl create pvc` command, followed by the necessary parameters to define the volume. For example, to create a volume that uses a local disk and has a capacity of 100GB, you could use the following command:

```
kubectl create pvc my-volume --capacity=100Gi --access-modes=ReadWriteOnce --storage-class=local-disk
```

To view the details of a volume, you can use the `kubectl describe pvc` command, followed by the name of the volume. This will display information about the volume, such as its capacity, access modes, and the PVCs that are associated with it.

To delete a volume, you can use the `kubectl delete pvc` command, followed by the name of the volume. This will delete the volume, as well as any PVCs that are associated with it.

### Volume Mode, Access Modes and Reclaim Policies for Volumes

In Kubernetes, **volume modes** are a way to control how persistent volumes (PVs) are accessed by applications. Volume modes determine how the PV is mounted, and whether it is read-only or read-write.

Volume modes are defined when a PV is created, and they can be specified using the kubectl command-line tool. The available volume modes for PVs in Kubernetes are:

* **Filesystem**: This is the default volume mode, and it indicates that the PV should be mounted as a file system.
* **Block**: This volume mode indicates that the PV should be mounted as a block device, which can be accessed at the block level rather than the file level.
* **Raw**: This volume mode indicates that the PV should be mounted as a raw block device, which allows direct access to the device without any filesystem formatting.

When you create a PV in Kubernetes, you can specify the volume mode that you want to use. This will determine how the PV is mounted, and it will affect how applications can access the PV. For more information, you can refer to the Kubernetes documentation.

In Kubernetes, persistent volumes (PVs) have different **access modes** that determine how they can be used by applications. The access mode of a PV determines which applications can access it, and how they can access it:

* **ReadWriteOnce**: This access mode allows a PV to be mounted as read-write by a single node. It is the most common access mode, and it is suitable for most workloads.
* **ReadOnlyMany**: This access mode allows a PV to be mounted as read-only by multiple nodes. It is useful for situations where multiple nodes need to read from the same data, such as with a distributed file system.
* **ReadWriteMany**: This access mode allows a PV to be mounted as read-write by multiple nodes. It is useful for situations where multiple nodes need to read and write to the same data, such as with a distributed database.

When you create a PV in Kubernetes, you can specify the access mode that you want to use. This will determine how the PV can be used by applications, and it will affect how the PV is provisioned and managed by Kubernetes. For more information, you can refer to the Kubernetes documentation.

In Kubernetes, persistent volumes (PVs) can have different reclaim policies that determine how they are handled when they are no longer needed by applications. Reclaim policies specify what should happen to the PV when the associated persistent volume claim (PVC) is deleted or released.

The available reclaim policies for PVs in Kubernetes are:

* **Retain**: This reclaim policy indicates that the PV should be retained when the associated PVC is deleted or released. The PV will not be deleted, and it can be manually reclaimed by an administrator.
* **Delete**: This reclaim policy indicates that the PV should be deleted when the associated PVC is deleted or released. The PV will be automatically deleted, and any data on the PV will be lost.
* **Recycle**: This reclaim policy indicates that the PV should be recycled when the associated PVC is deleted or released. The PV will be deleted and automatically recreated, allowing it to be used again by a new PVC.

When you create a PV in Kubernetes, you can specify the reclaim policy that you want to use. This will determine how the PV is handled when the associated PVC is deleted or released, and it will affect how the PV is managed by Kubernetes. For more information, you can refer to the Kubernetes documentation.

### Pnderstand Persistent Volume Claims

In Kubernetes, a **persistent volume claim (PVC)** is a way for an application to request a specific type and amount of storage. When a PVC is created, Kubernetes will automatically provision a persistent volume (PV) that matches the PVC's requirements, and it will bind the PVC to the PV. This allows the application to access the storage on the PV through the PVC.

A PVC is a "primitive" in the sense that it is a fundamental building block of the Kubernetes storage system. It is a declarative resource that specifies the storage requirements of an application, and it allows Kubernetes to automatically provision and manage the storage needed by the application.

To understand PVCs, it is important to understand the concept of PVs and how they are used in Kubernetes. PVs are the underlying storage resources that are managed by Kubernetes, and PVCs are the objects that applications use to request and access PVs.

For more information about PVCs and how they work in Kubernetes, you can refer to the Kubernetes documentation.

### Configure Applications with Persistent Storage

To configure an application with persistent storage in Kubernetes, you will need to create a persistent volume claim (PVC) for the application. A PVC is a way for an application to request a specific type and amount of storage, and it allows Kubernetes to automatically provision a persistent volume (PV) that matches the PVC's requirements.

To create a PVC for an application, you can use the kubectl command-line tool. For example, to create a PVC for an application that needs 100GB of storage on a local disk, you could use the following command:

```
kubectl create pvc my-pvc --capacity=100Gi --access-modes=ReadWriteOnce --storage-class=local-disk
````

This will create a PVC named my-pvc with the specified capacity and access modes, and it will use the local-disk storage class to provision the underlying PV. Once the PVC has been created, you can then use it to mount the PV as a volume in your application's deployment.
