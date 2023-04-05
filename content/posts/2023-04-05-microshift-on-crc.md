---
title: " Introducing MicroShift preset for CRC"
date: 2023-04-05T07:12:10+05:30
---

Are you a developer who wants to use OpenShift Kubernetes Engine but doesn't have a powerful system?
Or do you need to deploy to a small form factor or edge computing environment? 
If so, you'll be happy to hear about our new [MicroShift](https://access.redhat.com/documentation/en-us/red_hat_build_of_microshift/4.12/html/getting_started/index) preset,
a lightweight version of OpenShift Kubernetes Engine that's optimized for resource-limited environments.

The OpenShift preset currently provided by CRC requires 9GB of RAM and 4 CPUs.
With the release of CRC 2.16, you can now use the MicroShift preset, which only requires 4GB of RAM and 2 CPUs.

What makes MicroShift different from OpenShift Kubernetes Engine? MicroShift is designed for small form factor
and edge computing environments, which means it's optimized for lower resource requirements. MicroShift
uses a subset of the OpenShift Kubernetes Engine components and removes some of the features that aren't needed in these environments.

[Key differences from OpenShift Kubernetes Engine](https://access.redhat.com/documentation/en-us/red_hat_build_of_microshift/4.12/html/getting_started/microshift-architecture#microshift-differences-oke_microshift-architecture)

To get started with MicroShift, you'll need to download and install the [latest version](https://mirror.openshift.com/pub/openshift-v4/x86_64/clients/crc/latest) of CRC.
If you already have a CRC instance, delete it using the `crc delete` command.
Then set the preset to MicroShift using the `crc config set preset microshift` command.
Finally, set up and start CRC using the `crc setup` and `crc start` commands.
With crc version 2.16, in order to use the oc binary from `crc oc-env`, a [workaround](https://github.com/crc-org/crc/issues/3581#issuecomment-1497174956) is needed.

After CRC is started, a `kubeconfig` file will be generated, which is used to connect to the cluster.

To try out MicroShift, we've created a sample demo repository that you can find on [GitHub](https://github.com/praveenkumar/simple-go-server).
It includes step by step instructions to build and deploy a workload on a CRC instance using the MicroShift preset.

We'd love to hear your feedback and suggestions on the MicroShift preset. Please let us know in our [release discussion](https://github.com/orgs/crc-org/discussions/3584), or if you encounter any issues, please file them on our [issue tracker](https://github.com/crc-org/crc/issues).

In conclusion, MicroShift preset is a great option for users who need to use OpenShift Kubernetes Engine in resource-limited environments without some of the features of a Red Hat OpenShift cluster.
So give it a try and see how it can benefit you and your team!

