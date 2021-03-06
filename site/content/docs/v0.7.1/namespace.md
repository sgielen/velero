---
title: "Run in custom namespace"
layout: docs
---

In Ark version 0.7.0 and later, you can run Ark in any namespace. To do so, you specify the
namespace in the YAML files that configure the Ark server. You then also specify the namespace when
you run Ark client commands.

## Edit the example files

The Ark repository includes [a set of examples][0] that you can use to set up your Ark server. The
examples place the server in the `heptio-ark-server` namespace, and backup/schedule/restore/config
data in the `heptio-ark` namespace.

To run the server in another namespace, you edit the relevant files, changing `heptio-ark-server` to
your desired namespace.

To store your backups, schedules, restores, and config in another namespace, you edit the relevant
files, changing `heptio-ark` to your desired namespace.

WARNING: It is recommended to run the Ark server in one namespace, and place your backups, schedules,
restores, and config in a different namespace. You might encounter issues with deleting a single Ark
namespace that contains everything.

For all cloud providers, edit `https://github.com/heptio/ark/blob/main/examples/common/00-prereqs.yaml`. This file defines:

* CustomResourceDefinitions for the Ark objects (backups, schedules, restores, configs, downloadrequests)
* The namespace where the Ark server runs
* The namespace where backups, schedules, restores, and the config are stored
* The Ark service account
* The RBAC rules to grant permissions to the Ark service account


### AWS

For AWS, edit:

* `https://github.com/heptio/ark/blob/main/examples/common/10-deployment.yaml`
* `https://github.com/heptio/ark/blob/main/examples/aws/00-ark-config.yaml`


### GCP

For GCP, edit:

* `https://github.com/heptio/ark/blob/main/examples/common/10-deployment.yaml`
* `https://github.com/heptio/ark/blob/main/examples/gcp/00-ark-config.yaml`


### Azure

For Azure, edit:

* `https://github.com/heptio/ark/blob/main/examples/azure/00-ark-deployment.yaml`
* `https://github.com/heptio/ark/blob/main/examples/azure/10-ark-config.yaml`


## Specify the namespace in client commands

To specify the namespace for all Ark client commands, run:

```
ark client config set namespace=<NAMESPACE_VALUE>
```



[0]: https://github.com/heptio/ark/tree/main/examples
