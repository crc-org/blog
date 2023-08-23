---
title: "A Step-by-Step Guide to Creating the MicroShift next Bundle"
date: 2023-08-22T12:30:10+05:30
---

CRC is a tool that allows you to quickly and easily spin up a local OpenShift cluster.
It is a great way to learn about OpenShift/OKD/MicroShift and to test out new features.

If you're looking to experiment with the upcoming MicroShift release and want to learn
how to create the bundle to consume it with CRC, you're in the right place!
This blog post will guide you through the process step by step.

Prerequisites
-------------

To create a MicroShift bundle, you will need the following:
- A computer (or VM which have nested virtualization enabled) with RHEL-9 
- At least 60-70 GB of free disk space
- 4 CPUs
- 8 GB of memory

Getting the MicroShift Pre Release
----------------------------------

The first step is to make sure there is a MicroShift prerelease version available that you want to use. This information
is present at MicroShift GitHub repo
- https://github.com/openshift/MicroShift/releases

For example, the latest MicroShift version at the time of this writing is [4.14.0-ec.4](https://github.com/openshift/microshift/releases/tag/4.14.0-ec.4-202308011235.p0).

Cloning the SNC Repository
--------------------------
Next, you need to clone the SNC repository. This repository contains the scripts that you will use to create the bundle.
```bash
git clone https://github.com/crc-org/snc.git
```
**Note:** The master branch of snc always follows the latest Red Hat OpenShift Container Platform major release. For example, it's currently tracking RHOCP 4.13.x. To generate MicroShift bundles for prerelease, first switch to the appropriate branch:
```bash
git checkout origin/release-4.14
```

Getting the Pull Secret
------------------------
You need to have a pull secret that will be used for snc script. You can download this pull secret
from [here](https://console.redhat.com/openshift/create/local) using `Download Pull Secret` button.

Creating the Bundle
-------------------
You are now ready to create the bundle. You can do this by running the following command:
```bash
OPENSHIFT_PULL_SECRET_PATH=<downloaded_pull_secret_file_path> MICROSHIFT_PRERELEASE=yes ./microshift.sh
```
**Note: Wait till the `microshift` script finish successfully (takes around 30-40 mins)**
```bash
./createdisk.sh
```

**Congratulations! You've successfully created a prerelease version of MicroShift bundle**

Starting the Cluster
--------------------
Once you have created the bundle, you can start the cluster by running the following command:
```bash
crc setup --bundle crc_microshift_libvirt_4.14.0-ec.4_amd64.crcbundle
crc start --bundle crc_microshift_libvirt_4.14.0-ec.4_amd64.crcbundle
```

This will start the cluster with created MicroShift bundles. Once the cluster is started, you can follow the instructions at the end of start to access it.

Conclusion
----------
This blog post has shown you how to create a MicroShift bundle for prerelease and use it with CRC. By following these steps, you can quickly and easily spin up a local cluster using the prerelease version of MicroShift.
