# Developer Experience

OpenShift provides a platform for developers to deploy to Kubernetes.

This tutorial will demonstrate creating an application from source code.

## Creating an application from source code

To create a new project for your application, do the following:

```sh
oc new-project my-app
```

To build an application from source, push to the internal registry, and deploy, execute the following:

```sh
oc new-app centos/ruby-25-centos7~https://github.com/sclorg/ruby-ex.git
```

This will kick off a build of your source code on the platform to create an image.  The build is performed
in a pod using [buildah](https://github.com/containers/buildah).

To view the build logs, do the following:

```sh
oc logs -f bc/ruby-ex
```

After the build completes, the application deploys to the cluster.

To expose the application to your browser, do the following:

```sh
oc expose svc/ruby-ex
```

To get the URL for your application, do the following:

```sh
oc get routes ruby-ex -o jsonpath='{"http://"}{.spec.host}{"/"}{"\n"}' 
https://ruby-ex-my-app.apps.example.com/
```

Open the browser, and see your application!

Next: [Explore More](../03-explore.md)