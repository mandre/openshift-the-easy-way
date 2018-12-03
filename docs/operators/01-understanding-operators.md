# Understanding operators

An Operator is a method of packaging, deploying and managing a Kubernetes
application.  A Kubernetes application is an application that is both deployed
on Kubernetes and managed using the Kubernetes APIs.

## Managing the platform

Kubernetes does a great job managing a containerized application through
powerful, declarative automation primitives.

OpenShift provides a `ClusterVersionOperator` that manages a set of operators to
install, update, and lifecycle Kubernetes itself.  These operators allow us to
manage the core control plane components as a Kubernetes native application.  The
`ClusterVersionOperator` manages a minimal set of components required to bring up
an OpenShift service.

## Managing applications on the platform

Applications that run on the platform have the same install, update, and lifecycle
managment problems as the control plane itself.  OpenShift provides the `Operator Lifecycle Manager` component to enable
administrators to deploy optional parts of the OpenShift distribution while still maintaining
the operatational benefits associated with operators.

# Next steps

The following section will describe each class of operator in more detail.

Next: [Cluster Version Operator](02-cluster-version-operator.md)