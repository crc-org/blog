---
title: "How to use bundle option"
date: 2024-03-22T12:39:10+05:30
---

CRC provides a config option called `bundle` to configure the _location_ of the bundle. This option is useful when you
want to use a bundle that is not the default one or user want to try a bundle which is not part of release but available
at the OpenShift mirror location. The `bundle` option can accept local filesystem paths, container registry URLs, and
http/https URLs. This blog post will guide you through the process of using the `bundle` option using config or
setup/start commands.

## Using `bundle` option with `crc config` command

You can use the `crc config set bundle` command to set the bundle location. This command can accept local filesystem paths,
container registry URLs, and http/https URLs. Here are some examples:

```bash
# Assume user want to use microshift-4.15.0 bundle which is not part of crc release but available at the OpenShift mirror location
crc config set bundle https://developers.redhat.com/content-gateway/file/pub/openshift-v4/clients/crc/bundles/microshift/4.15.0/crc_microshift_libvirt_4.15.0_amd64.crcbundle
crc setup
crc start
```

## Using `bundle` option with `crc setup` and `crc start` commands
```bash
crc setup --bundle https://developers.redhat.com/content-gateway/file/pub/openshift-v4/clients/crc/bundles/microshift/4.15.0/crc_microshift_libvirt_4.15.0_amd64.crcbundle
crc start --bundle https://developers.redhat.com/content-gateway/file/pub/openshift-v4/clients/crc/bundles/microshift/4.15.0/crc_microshift_libvirt_4.15.0_amd64.crcbundle
```

**Beware**, if you use -b https:// there will be no signature checks
Bundles downloaded from mirror.openshift.com can be verified this way:
```bash
curl -L -O https://developers.redhat.com/content-gateway/file/pub/openshift-v4/clients/crc/bundles/microshift/4.15.0/crc_microshift_libvirt_4.15.0_amd64.crcbundle
curl -L -O https://developers.redhat.com/content-gateway/file/pub/openshift-v4/clients/crc/bundles/microshift/4.15.0/crc_microshift_libvirt_4.15.0_amd64.crcbundle.sha256
sha256sum crc_microshift_libvirt_4.15.0_amd64.crcbundle => should match with the content of crc_microshift_libvirt_4.15.0_amd64.crcbundle.sha256
```

## Conclusion
This blog post has shown you how to use the `bundle` option with CRC. By following these steps, you can quickly and easily
spin up a local cluster using the bundle of your choice.
As usual, we'd like to get your [feedback](https://github.com/crc-org/crc/issues/new/choose) on all this work!