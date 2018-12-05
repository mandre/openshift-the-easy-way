# OpenShift Cluster Monitoring

OpenShift Container Platform ships with a pre-configured and self-updating
monitoring stack that is based on the Prometheus open source project and its
wider eco-system. It provides monitoring of cluster components and ships with a
set of alerts to immediately notify the cluster administrator about any
occurring problems and a set of Grafana dashboards.

# Accessing Prometheus

To access Prometheus, visit the URL from the following:

```sh
oc get routes -n openshift-monitoring prometheus-k8s -o jsonpath='{"https://"}{.spec.host}{"/"}{"\n"}'
```

If you are prompted to login, login with OpenShift, and follow the oauth flow.

To view the list of endpoints scraped, click `Status`->`Targets`.

To view the list of out of the box alerts, click `Alerts`.

To execute a sample query, click `Graph`.

Enter:

```
sum(
    rate(container_cpu_usage_seconds_total[5m]))
by (container_name)
```

Click `Execute`

This shows containers that used the most CPU on the platform over last 5
minutes.

# Accessing Grafana

To access Grafana, visit the URL from the following:

```sh
oc get routes -n openshift-monitoring grafana -o jsonpath='{"https://"}{.spec.host}{"/"}{"\n"}'
```

Click `Dashboards` -> `Manage` and see the list of out of the box dashboards
showing usage of resources in the cluster.

Next: [Explore More](../03-explore.md)