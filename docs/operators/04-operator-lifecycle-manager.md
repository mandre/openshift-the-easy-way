# Operator Lifecycle Manager

[Operator Lifecycle Manager](https://github.com/operator-framework/operator-lifecycle-manager)
is a management framework for extending Kubernetes with operators.  Administrators
are able to deploy optional components that are managed by an operator into the cluster.

In this tutorial, we will deploy a few operators to the cluster.

## Catalog Sources

list catalog sources
```sh
$ oc get catalogsources -n openshift-operator-lifecycle-manager
NAME                  NAME                  TYPE       PUBLISHER   AGE
certified-operators   Certified Operators   internal   Red Hat     53m
rh-operators          Red Hat Operators     internal   Red Hat     53m
```

## Subscriptions

### Federation-v2

The [Federation-v2 Operator](https://github.com/openshift/federation-v2-operator) manages
the deployment of the Kubernetes [Federation-v2](https://github.com/kubernetes-sigs/federation-v2)
project.

Users consume applications in their namespaces by creating **Subscriptions**:

```sh
oc create -f https://raw.githubusercontent.com/derekwaynecarr/openshift-the-easy-way/master/assets/subscription-federation-v2.yaml
```

### Etcd

Add more text

```sh
oc new-project my-project
oc create -f ../../derekwaynecarr/openshift-the-easy-way/assets/subscription-etcd.yaml 
subscription.operators.coreos.com/etcd created
oc create -f ../../derekwaynecarr/openshift-the-easy-way/assets/etcd-cluster.yaml
```

### Descheduler

Add descheduler

Next: [Configuration](04-configuration.md)