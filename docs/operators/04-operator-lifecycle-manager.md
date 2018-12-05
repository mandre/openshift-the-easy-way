# Operator Lifecycle Manager

[Operator Lifecycle
Manager](https://github.com/operator-framework/operator-lifecycle-manager) is a
management framework for extending Kubernetes with operators.  Administrators
are able to deploy optional components that are managed by an operator into the
cluster.

In this tutorial, we will deploy a few operators to the cluster.

# Kubernetes Marketplace

The marketplace provides a catalog of operators provided by Red Hat and others.

To explore the marketplace via the web console, open the following url in a
browser:

```sh
oc get routes -n openshift-console console -o jsonpath='{"https://"}{.spec.host}{"/marketplace"}{"\n"}'
https://console-openshift-console.apps.example.com/marketplace
```

## Package Manifests

Operators are packaged into a set of manifests.

To view the package manifests, do the following:

```sh
oc get packagemanifests
NAME                   AGE
amq-streams            43m
etcd                   43m
federationv2           43m
prometheus             43m
svcat                  43m
couchbase-enterprise   43m
dynatrace-monitoring   43m
mongodb-enterprise     43m
```

## Subscriptions

Users consume applications in their namespaces by creating `Subscription`
resources.  Each subscription subscribes to channels so operators automatically
update when new versions are released.

### Federation-v2

The [Federation-v2
Operator](https://github.com/openshift/federation-v2-operator) manages the
deployment of the Kubernetes
[Federation-v2](https://github.com/kubernetes-sigs/federation-v2) project.

```sh
oc create -f https://raw.githubusercontent.com/derekwaynecarr/openshift-the-easy-way/master/assets/subscription-federation-v2.yaml
```

The federation v2 function provides a cluster registry via a `Cluster` resource.

To register a cluster in the `Cluster` registry, you can do the following:

```sh
oc create -f https://raw.githubusercontent.com/derekwaynecarr/openshift-the-easy-way/master/assets/federation-v2-registry.yaml
```

### Etcd

The [Etcd Operator](https://github.com/coreos/etcd-operator) manages the deployment
of `etcd` on Kubernetes clusters.  Once deployed on the cluster, it enables users
to create new resources using the `EtcdCluster` custom resource definition, and then
take backups via the `EtcdBackup` or perform restores via the `EtcdRestore` resources.

To deploy the etcd operator, execute the following:

```sh
oc create -f https://raw.githubusercontent.com/derekwaynecarr/openshift-the-easy-way/master/assets/subscription-etcd.yaml
```

To create a etcd cluster using the operator, execute the following:

```sh
oc create -f https://raw.githubusercontent.com/derekwaynecarr/openshift-the-easy-way/master/assets/etcd-cluster.yaml
```

To view etcd running in the project, execute the following:

```sh
oc describe etcdcluster -n my-operators
Name:         example
Namespace:    my-operators
Labels:       <none>
Annotations:  <none>
API Version:  etcd.database.coreos.com/v1beta2
Kind:         EtcdCluster
Metadata:
  Creation Timestamp:  2018-12-05T20:27:39Z
  Generation:          1
  Resource Version:    52492
  Self Link:           /apis/etcd.database.coreos.com/v1beta2/namespaces/my-operators/etcdclusters/example
  UID:                 35f5ec57-f8cc-11e8-aa1b-02f937e7bba4
Spec:
  Repository:  quay.io/coreos/etcd
  Size:        3
  Version:     3.2.13
Status:
  Client Port:  2379
  Conditions:
    Last Transition Time:  2018-12-05T20:27:55Z
    Last Update Time:      2018-12-05T20:27:55Z
    Message:               Current cluster size: 1, desired cluster size: 3
    Reason:                Scaling up
    Status:                True
    Type:                  Scaling
  Current Version:         
  Members:
    Ready:
      example-sm2jnqfg9j
  Phase:           Running
  Service Name:    example-client
  Size:            2
  Target Version:  
Events:
  Type    Reason            Age   From                            Message
  ----    ------            ----  ----                            -------
  Normal  New Member Added  1m    etcd-operator-68b4997899-xtdsp  New member example-sm2jnqfg9j added to cluster
  Normal  New Member Added  44s   etcd-operator-68b4997899-xtdsp  New member example-nvpgfnxnx7 added to cluster
```

Next: [Explore More](../03-explore.md)