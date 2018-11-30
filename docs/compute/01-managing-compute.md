# Managing Compute

This tutorial will walk you through managing compute instances.

## Bootstrapping

The installer provisions the required infrastructure to run the cluster.

The installer creates a highly-available control plane by creating `master` machine in each zone.

After the control plane is bootstrapped, OpenShift uses the machine API types
introduced by the [Kubernetes Cluster API](https://github.com/kubernetes-sigs/cluster-api) to
adopt those machines and bring them under management of the cluster.

To see the machines, you can run the following command:

```sh
oc get machines -n openshift-cluster-api
NAME                             AGE
decarr-master-0                  3h
decarr-master-1                  3h
decarr-master-2                  3h
decarr-worker-us-east-2a-gdbnm   3h
decarr-worker-us-east-2b-bj9dz   3h
decarr-worker-us-east-2c-w2pfs   3h
```

## Control Plane

The control plane is executed on machines that have the `sigs.k8s.io/cluter-api-machine-type=master` label.

To find all machines that run the control plane, execute the following:

```sh
oc get machines -l sigs.k8s.io/cluster-api-machine-type=master -n openshift-cluster-api
NAME              AGE
decarr-master-0   3h
decarr-master-1   3h
decarr-master-2   3h
```

The nodes that run the control plane are special and are not backed by machine controller.

Similar to pods, the cluster runs a control loop to ensure the master nodes always exist.

## Workers

The worker nodes run end-user workloads on the cluster.

They execute on machines that have the `sigs.k8s.io/cluster-api-machine-type=worker` label.

To find all worker machines, execute the following:

```sh
oc get machines -l sigs.k8s.io/cluster-api-machine-type=worker -n openshift-cluster-api
NAME                             AGE
decarr-worker-us-east-2a-gdbnm   4h
decarr-worker-us-east-2b-bj9dz   4h
decarr-worker-us-east-2c-w2pfs   4h
```

For each worker machine, you can find out provider specific information in its providerConfig.

For example, on a cluster installed on `Amazon Web Services`, you can see the instance type, zone, and region.

```sh
oc get machines -n openshift-cluster-api -o jsonpath='{range .items[*]}{"\n"}{.metadata.name}{"\t"}{.spec.providerConfig.value.instanceType}{end}{"\n"}'
```

Unlike control plane nodes, worker nodes are backed by the `MachineSet` machine controller.

To view all machine sets, execute the following:

```sh
oc get machinesets -n openshift-cluster-api
NAME                       AGE
decarr-worker-us-east-2a   5h
decarr-worker-us-east-2b   5h
decarr-worker-us-east-2c   5h
```

A `MachineSet` ensures a desired number of replica `Machines` exist similar to a `ReplicaSet` ensuring a desired number of `Pods`.

To view the number of replicas for each `MachineSet`, execute the following:


```sh
oc get machinesets -n openshift-cluster-api -o jsonpath='{range .items[*]}{"\n"}{.metadata.name}{"\t"}{.status.replicas}{end}{"\n"}'
decarr-worker-us-east-2a	1
decarr-worker-us-east-2b	1
decarr-worker-us-east-2c	1
```

Each machine set manages a pool of nodes in a given region and zone.

Users are able to construct new `MachineSets` that reference different classes of machine types.

The `MachineSet` construct enables primitives to perform scaling and health checks across a pool of common machines.

Next: [Cluster Autoscaling](02-cluster-autoscaling.md)