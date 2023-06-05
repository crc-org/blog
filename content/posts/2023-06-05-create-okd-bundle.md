---
title: "How to create OKD bundle"
date: 2023-06-05T11:43:10+05:30
---

CRC is a tool that allows you to quickly and easily spin up a local OpenShift cluster.
It is a great way to learn about OpenShift/OKD/MicroShift and to test out new features.

In this blog post, we will explain to you, how to create an OKD bundle for CRC.

Prerequisites
-------------

To create an OKD bundle, you will need the following:
- A computer with a recent version of Fedora, CentOS Stream or RHEL
- At least 60-70 GB of free disk space
- 8 CPUs
- 24 GB of memory

Getting the OKD Release
----------------------

The first step is to get the OKD release version that you want to use. This information is present at OKD GitHub repo
- https://github.com/okd-project/okd/releases 

For example, the latest OKD version at the time of this writing is [4.13.0-0.okd-2023-06-04-080300](https://github.com/okd-project/okd/releases/tag/4.13.0-0.okd-2023-06-04-080300), this version number will be needed in the following steps.

Cloning the SNC Repository
--------------------------
Next, you need to clone the SNC repository. This repository contains the scripts that you will use to create the bundle.
```bash
git clone https://github.com/crc-org/snc.git
```
**Note:** The master branch of snc always follows the latest Red Hat OpenShift Container Platform major release. For example it's currently tracking RHOCP 4.13.x. To generate OKD bundles for older releases, first switch to the appropriate branch:
```bash
git checkout origin/release-4.12
```

Setting the OKD Version
-----------------------
You need to set the OKD_VERSION environment variable to the version of OKD that you want to use.
```bash
export OKD_VERSION=4.12.0-0.okd-2023-04-16-041331
```

Creating the Pull Secret
------------------------
You need to create a dummy pull secret that will be used for snc script. You can create this dummmy pull secret using the following command:
```bash
cat <<EOF > pullsecret.json
{
  "auths": {
    "fake": {
      "auth": "Zm9vOmJhcgo="
    }
  }
}
EOF
```

Creating the Bundle
-------------------
You are now ready to create the bundle. You can do this by running the following command:
```bash
OPENSHIFT_PULL_SECRET_PATH=pullsecret.json ./snc.sh
```
**Note: Wait till the `snc.sh` script finish successfully (takes around 40-50 mins)**
```bash
./createdisk.sh
```

Starting the Cluster
--------------------
Once you have created the bundle, you can start the cluster by running the following command:
```bash
crc setup --bundle crc_okd_libvirt_4.12.0-0.okd-2023-04-16-041331_amd64.crcbundle
crc start --bundle crc_okd_libvirt_4.12.0-0.okd-2023-04-16-041331_amd64.crcbundle
```

This will start the cluster with created OKD bundles. Once the cluster is started, you can follow the instructions at the end of start to access it.

Conclusion
----------
This blog post has shown you how to create an OKD bundle for CRC. By following these steps, you can quickly and easily spin up a local cluster using the version of OKD that you want.
