# Install

The OpenShift Installer is designed to help users, ranging from novices to
experts, create OpenShift clusters in various environments. By default, the
installer acts as an installation wizard, prompting the user for values that it
cannot determine on its own and providing reasonable defaults for everything
else. For more advanced users, the installer provides facilities for varying
levels of customization.

In [supported environments][supported-environments], the installer is also
capable of provisioning the underlying infrastructure for the cluster. It is
recommended that most users make use of this functionality in order to avoid
having to provision their own infrastructure. In unsupported environments or
scenarios in which installer-created infrastructure would be incompatible, the
installer can stop short of creating the infrastructure, and allow the user to
provision their own infrastructure using the cluster assets generated by the
installer.

## Prerequisites

In the prior step, we downloaded the following:

1. installer (e.g. `openshift-install-linux-amd64`)
1. pull secret (e.g. `~/Downloads/pull-secret`)

## Wizard

The installer provides a guided experience for provisioning the cluster on a
particular platform.  

After approximately 10 minutes, you should have a highly available cluster with
3 masters and 3 workers.

### Linux

The following demonstrates an install using the wizard as an example.

```
./openshift-install-linux-amd64 create cluster
? Email Address user@example.com
? Password [? for help] ********
? SSH Public Key ~/.ssh/id_rsa.pub
? Base Domain dev.example.com
? Cluster Name my-cluster
? Pull Secret [? for help] ******
? Platform aws
? Region us-east-2
INFO Creating cluster...                          
INFO Waiting 30m0s for the Kubernetes API...      
INFO API v1.11.0+99b66db up                       
INFO Waiting 30m0s for the bootstrap-complete event... 
INFO Destroying the bootstrap resources...        
INFO Using Terraform to destroy bootstrap resources... 
INFO kubeadmin user password: Seiv2-q9xJW-2rHR2-UGRRj 
INFO Install complete! The kubeconfig is located here: /home/decarr/go/src/github.com/openshift/installer/auth/kubeconfig 
```

### Mac

The following demonstrates an install using the wizard as an example.

```
./openshift-install-darwin-amd64 create cluster
? Email Address user@example.com
? Password [? for help] ********
? SSH Public Key ~/.ssh/id_rsa.pub
? Base Domain dev.example.com
? Cluster Name my-cluster
? Pull Secret [? for help] ******
? Platform aws
? Region us-east-2
INFO Creating cluster...                          
INFO Waiting 30m0s for the Kubernetes API...      
INFO API v1.11.0+99b66db up                       
INFO Waiting 30m0s for the bootstrap-complete event... 
INFO Destroying the bootstrap resources...        
INFO Using Terraform to destroy bootstrap resources... 
INFO kubeadmin user password: Seiv2-q9xJW-2rHR2-UGRRj 
INFO Install complete! The kubeconfig is located here: /home/decarr/go/src/github.com/openshift/installer/auth/kubeconfig
```

## Multiple Invocations

If you want to avoid the wizard in future runs, you can [save the generated `install-config.yaml` and reuse it later][multiple-invocations].

Next: [Exploring the Cluster](03-explore.md)

[multiple-invocations]: https://github.com/openshift/installer/blob/master/docs/user/overview.md#multiple-invocations
[supported-environments]: https://github.com/openshift/installer/blob/master/README.md#supported-platforms
