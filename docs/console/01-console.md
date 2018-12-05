# OpenShift Console

The web console is a user interface accessible from a web browser that lets you explore the cluster.

## Accessing the console

The web console is accessible via a `Route`.

To access the console:

```sh
oc get routes -n openshift-console console -o jsonpath='{"https://"}{.spec.host}{"\n"}'
https://console-openshift-console.apps.mycluster.example.com
```

## Login to the cluster

The install creates a transient admin user `kubeadmin`.

The password for this user is output by the install.

To view the password, do the following:

```sh
cat ./auth/kubeadmin-password
```

Login to the cluster using `kubeadmin` and the password above.

Click `Projects` and explore.

Next: [Explore More](../03-explore.md)