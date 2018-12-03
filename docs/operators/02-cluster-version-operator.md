# Cluster Version Operator

This tutorial describes the top level operator that manages cluser updates.

## Cluster Version Operator

This operator manages cluster updates.  It continously reconciles an update
payload with the Kubernetes API server to ensure the desired cluster version is
the actual version.

To view the operator, execute the following:

```sh
oc get deployments -n openshift-cluster-version
NAME                       DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
cluster-version-operator   1         1         1            1           1h
```

## Release Update Payload

The update payload is built into the cluster version operator image.

To view the release update payload, execute the following:

```sh
oc get pods -n openshift-cluster-version
NAME                                       READY     STATUS    RESTARTS   AGE
cluster-version-operator-8bb6cff75-j6n5k   1/1       Running   0          1h
oc exec -n openshift-cluster-version -it cluster-version-operator-8bb6cff75-j6n5k /bin/
sh-4.2# ls release-manifests
0000_07_cluster-network-operator_00_namespace.yaml				       0000_50_machine-api-operator_00_namespace.yaml
0000_07_cluster-network-operator_01_crd.yaml					       0000_50_machine-api-operator_01_images.configmap.yaml
0000_07_cluster-network-operator_02_rbac.yaml					       0000_50_machine-api-operator_02_machine.crd.yaml
0000_07_cluster-network-operator_03_daemonset.yaml				       0000_50_machine-api-operator_03_machineset.crd.yaml
0000_08_cluster-dns-operator_00-cluster-role.yaml				       0000_50_machine-api-operator_04_machinedeployment.crd.yaml
0000_08_cluster-dns-operator_00-custom-resource-definition.yaml			       0000_50_machine-api-operator_05_cluster.crd.yaml
0000_08_cluster-dns-operator_00-namespace.yaml					       0000_50_machine-api-operator_06_machineclass.crd.yaml
0000_08_cluster-dns-operator_01-cluster-role-binding.yaml			       0000_50_machine-api-operator_07_machinehealthcheck.crd.yaml
0000_08_cluster-dns-operator_01-role-binding.yaml				       0000_50_machine-api-operator_08_rbac.yaml
0000_08_cluster-dns-operator_01-role.yaml					       0000_50_machine-api-operator_09_deployment.yaml
0000_08_cluster-dns-operator_01-service-account.yaml				       0000_50_machine-config-operator_00_namespace.yaml
0000_08_cluster-dns-operator_02-deployment.yaml					       0000_50_machine-config-operator_01_mcoconfig.crd.yaml
0000_09_service-serving-cert-signer_00_roles.yaml				       0000_50_machine-config-operator_02_images.configmap.yaml
0000_09_service-serving-cert-signer_01_namespace.yaml				       0000_50_machine-config-operator_03_rbac.yaml
0000_09_service-serving-cert-signer_02_crd.yaml					       0000_50_machine-config-operator_04_deployment.yaml
0000_09_service-serving-cert-signer_03_cm.yaml					       0000_51_machine-approver-00-ns.yaml
0000_09_service-serving-cert-signer_04_sa.yaml					       0000_51_machine-approver-01-sa.yaml
0000_09_service-serving-cert-signer_05_deploy.yaml				       0000_51_machine-approver-02-clusterrole.yaml
0000_09_service-serving-cert-signer_06_config.yaml				       0000_51_machine-approver-03-clusterrolebinding.yaml
0000_10_cluster-kube-apiserver-operator_00_namespace.yaml			       0000_51_machine-approver-04-deployment.yaml
0000_10_cluster-kube-apiserver-operator_01_config.crd.yaml			       0000_70_cluster-image-registry-operator_00-crd.yaml
0000_10_cluster-kube-apiserver-operator_02_service.yaml				       0000_70_cluster-image-registry-operator_01-namespace.yaml
0000_10_cluster-kube-apiserver-operator_03_configmap.yaml			       0000_70_cluster-image-registry-operator_01-openshift-config-managed-namespace.yaml
0000_10_cluster-kube-apiserver-operator_04_clusterrolebinding.yaml		       0000_70_cluster-image-registry-operator_01-openshift-config-namespace.yaml
0000_10_cluster-kube-apiserver-operator_05_serviceaccount.yaml			       0000_70_cluster-image-registry-operator_02-rbac.yaml
0000_10_cluster-kube-apiserver-operator_06_deployment.yaml			       0000_70_cluster-image-registry-operator_03-sa.yaml
0000_11_cluster-kube-scheduler-operator_00_namespace.yaml			       0000_70_cluster-image-registry-operator_04-operator.yaml
0000_11_cluster-kube-scheduler-operator_01_config.crd.yaml			       0000_70_cluster-image-registry-operator_05-ca-config.yaml
0000_11_cluster-kube-scheduler-operator_03_configmap.yaml			       0000_70_cluster-image-registry-operator_06-ca-rbac.yaml
0000_11_cluster-kube-scheduler-operator_04_clusterrolebinding.yaml		       0000_70_cluster-image-registry-operator_07-ca-serviceaccount.yaml
0000_11_cluster-kube-scheduler-operator_05_serviceaccount.yaml			       0000_70_cluster-image-registry-operator_08-ca-daemonset.yaml
0000_11_cluster-kube-scheduler-operator_06_deployment.yaml			       0000_70_cluster-ingress-operator_00-cluster-role.yaml
0000_12_cluster-kube-controller-manager-operator_00_namespace.yaml		       0000_70_cluster-ingress-operator_00-custom-resource-definition.yaml
0000_12_cluster-kube-controller-manager-operator_01_config.crd.yaml		       0000_70_cluster-ingress-operator_00-namespace.yaml
0000_12_cluster-kube-controller-manager-operator_02_service.yaml		       0000_70_cluster-ingress-operator_01-cluster-role-binding.yaml
0000_12_cluster-kube-controller-manager-operator_03_configmap.yaml		       0000_70_cluster-ingress-operator_01-kube-system-aws-creds-role-binding.yaml
0000_12_cluster-kube-controller-manager-operator_04_clusterrolebinding.yaml	       0000_70_cluster-ingress-operator_01-role-binding.yaml
0000_12_cluster-kube-controller-manager-operator_05_serviceaccount.yaml		       0000_70_cluster-ingress-operator_01-role.yaml
0000_12_cluster-kube-controller-manager-operator_06_deployment.yaml		       0000_70_cluster-ingress-operator_01-service-account.yaml
0000_20_cluster-openshift-apiserver-operator_00_namespace.yaml			       0000_70_cluster-ingress-operator_02-deployment.yaml
0000_20_cluster-openshift-apiserver-operator_01_config.crd.yaml			       0000_70_cluster-monitoring-operator_01-namespace.yaml
0000_20_cluster-openshift-apiserver-operator_03_configmap.yaml			       0000_70_cluster-monitoring-operator_02-role-binding.yaml
0000_20_cluster-openshift-apiserver-operator_04_roles.yaml			       0000_70_cluster-monitoring-operator_02-role.yaml
0000_20_cluster-openshift-apiserver-operator_05_serviceaccount.yaml		       0000_70_cluster-monitoring-operator_03-config.yaml
0000_20_cluster-openshift-apiserver-operator_06_service.yaml			       0000_70_cluster-monitoring-operator_03-etcd-secret.yaml
0000_20_cluster-openshift-apiserver-operator_07_deployment.yaml			       0000_70_cluster-monitoring-operator_04-deployment.yaml
0000_21_cluster-openshift-controller-manager-operator_00_namespace.yaml		       0000_70_cluster-node-tuning-operator_01-namespace.yaml
0000_21_cluster-openshift-controller-manager-operator_01_config.crd.yaml	       0000_70_cluster-node-tuning-operator_02-crd.yaml
0000_21_cluster-openshift-controller-manager-operator_02_configmap.yaml		       0000_70_cluster-node-tuning-operator_03-rbac.yaml
0000_21_cluster-openshift-controller-manager-operator_03_builder-deployer-config.yaml  0000_70_cluster-node-tuning-operator_04-operator.yaml
0000_21_cluster-openshift-controller-manager-operator_04_roles.yaml		       0000_70_cluster-samples-operator_00-crd.yaml
0000_21_cluster-openshift-controller-manager-operator_05_serviceaccount.yaml	       0000_70_cluster-samples-operator_01-namespace.yaml
0000_21_cluster-openshift-controller-manager-operator_06_build.crd.yaml		       0000_70_cluster-samples-operator_02-sa.yaml
0000_21_cluster-openshift-controller-manager-operator_07_deployment.yaml	       0000_70_cluster-samples-operator_03-rbac.yaml
0000_30_00-namespace.yaml							       0000_70_cluster-samples-operator_04-openshift-rbac.yaml
0000_30_01-olm-operator.serviceaccount.yaml					       0000_70_cluster-samples-operator_05-operator.yaml
0000_30_02-clusterserviceversion.crd.yaml					       0000_70_console-operator_00-crd.yaml
0000_30_03-installplan.crd.yaml							       0000_70_console-operator_00-oauth.yaml
0000_30_04-subscription.crd.yaml						       0000_70_console-operator_01-namespace.yaml
0000_30_05-catalogsource.crd.yaml						       0000_70_console-operator_02-rbac-role.yaml
0000_30_06-rh-operators.configmap.yaml						       0000_70_console-operator_03-rbac-rolebinding.yaml
0000_30_07-certified-operators.configmap.yaml					       0000_70_console-operator_04-config.yaml
0000_30_08-certified-operators.catalogsource.yaml				       0000_70_console-operator_04-sa.yaml
0000_30_09-rh-operators.catalogsource.yaml					       0000_70_console-operator_05-operator.yaml
0000_30_10-olm-operator.deployment.yaml						       0000_70_csi-operator_01_crd.yaml
0000_30_11-catalog-operator.deployment.yaml					       0000_70_csi-operator_02_csi_roles.yaml
0000_30_12-aggregated.clusterrole.yaml						       0000_70_csi-operator_03_csi_operator_role.yaml
0000_30_13-packageserver.yaml							       0000_70_csi-operator_04_namespace.yaml
0000_30_14-operatorgroup.crd.yaml						       0000_70_csi-operator_05_sa.yaml
0000_50_cluster-autoscaler-operator_00_namespace.yaml				       0000_70_csi-operator_06_role_binding.yaml
0000_50_cluster-autoscaler-operator_01_clusterautoscaler.crd.yaml		       0000_70_csi-operator_07_config.yaml
0000_50_cluster-autoscaler-operator_02_machineautoscaler.crd.yaml		       0000_70_csi-operator_99_operator.yaml
0000_50_cluster-autoscaler-operator_03_rbac.yaml				       image-references
0000_50_cluster-autoscaler-operator_04_deployment.yaml
```

## Understanding Upgrades

To upgrade the cluster is to update cluster version operator release image.

The new version of the operator embeds an updated set of release payloads that it will
apply to the cluster.  This simplifies cluster upgrades into a series of `kubectl apply`
statements that represent the desired state that each operator converges against.  Since
operators reconcile desired state with observed state, the cluster version operator helps
prevent drift of the cluster configuration.

As an operator, you understand and trust that the system will converge like any other
application you deploy to the cluster.

## Cluster Version

To view the version of the cluster, access the `ClusterVersion` resource.

```sh
oc get clusterversion
NAME      VERSION                           AVAILABLE   PROGRESSING   SINCE     STATUS
version   4.0.0-0.alpha-2018-12-03-184540   True        False         1h        Cluster version is 4.0.0-0.alpha-2018-12-03-184540
```

## Second Level Operators

The cluster version operator manages a set of second level operators that know how to manage
a particular binary or service required to run the cluster.  As a result, we call these operators
second level operators.

Each operator manages a particular binary or service needed to run the cluster.

To view the list of cluster operators and their status, execute the following:

```sh
oc get clusteroperators
NAME                                                      VERSION                         AVAILABLE   PROGRESSING   SINCE
machine-api-operator                                      v0.0.0-was-not-built-properly   True                      1m
machine-config-operator                                   3.11.0-294-g77b0e7bc-dirty      True        False         16s
openshift-cluster-kube-scheduler-operator                                                                           
openshift-cluster-openshift-controller-manager-operator   3.11.0                          True        False         
openshift-cluster-samples-operator                                                        True        False         1h
```
**TODO** UPDATE THIS SECTION WITH FULL LIST

# Next steps

Optional components that administrators can install in the distribution are
managed by Operator Lifecycle Manager.

Next: [Operator Lifecycle Management](03-operator-lifecycle-manager.md)