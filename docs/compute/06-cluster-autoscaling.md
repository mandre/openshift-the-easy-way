# Cluster Autoscaling

## Operator

OpenShift ships an operator that can manage deployment of the Cluster Autoscaler
component.

To view the operator, execute the following:

```sh
oc get deployments -n openshift-cluster-api cluster-autoscaler-operator
NAME                          DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
cluster-autoscaler-operator   1         1         1            1           1h
```

## Deploy Cluster Autoscaler

The operator watches for a `ClusterAutoscaler` resource to know how to deploy
the autoscaler.  The `ClusterAutoscaler` resource allows operators to configure
how the autoscaler is deployed to control its behavior.  For example, users are
able to bound the maximum size of the cluster, control if the autoscaler ever
scales down, or the minimum pod priority for when the autoscaler chooses to
scale up.

The sample configuration [file](../assets/cluster-autoscaler.yaml) for a
`ClusterAutoscaler` object that restricts the cluster from scaling above 24 nodes.

To deploy the cluster autoscaler, execute the following:

```sh
oc create -f https://raw.githubusercontent.com/openshift/cluster-autoscaler-operator/master/examples/clusterautoscaler.yaml
```

To verify the cluster autoscaler is deployed, execute the following:

```sh
oc get deployments cluster-autoscaler-default -n openshift-cluster-api
NAME                         DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
cluster-autoscaler-default   1         1         1            1           3m
```

## Scaling Workers

TODO

Next: [Machine Health Checks](03-machine-health-checks.md)