# Developer Experience

## Creating an Application From Source Code

```sh
oc new-app https://github.com/sclorg/cakephp-ex
```

Follow the build logs for your source code.

```sh
oc logs -f bc/cakephp-ex
```

Show pods running

```sh
oc get pods
```

**BLOCKED:** waiting on new build

visit

Next: [Explore More](../03-explore.md)