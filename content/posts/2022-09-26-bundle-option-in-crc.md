---
title: "Different bundle types option in crc"
date: 2022-09-26T10:41:10+05:30
---

CRC provides a config option called `bundle` to configure the _location_ of the bundle, 
until 2.9 release of CRC the bundle option could only accept local filesystem path
which meant users needed to download the bundle in advance before consuming it. The move to a
container registry for hosting the okd and podman bundles, introduces another step in the
process as bundles are now generated as an OCI container image and the *.crcbundle file
needs to be extracted from the image.

Since this adds significant friction for users wanting to use different bundles, we decided
to extend the bundle config option to also support container registry urls and http/https urls
in addition to local filesystem paths.

Starting with CRC 2.9.0 release, `bundle` config option supports three different way to configure
bundle location, these are explained below with use cases.

Case 1: If users want to use their own internal container registry for podman/okd bundles then they can
_copy_ the bundle images from `quay.io` to their internal container registry using [skopeo](https://github.com/containers/skopeo).
```bash
# Copy latest 4.2.0 podman bundle to internal registry
$  skopeo copy -a docker://quay.io/crcont/podman-bundle:4.2.0 docker://<internal_registry>/podman-bundle:4.2.0

$ crc config set bundle docker://<internal_registry>/podman-bundle:4.2.0
$ crc config set preset podman
$ crc setup
$ crc start
```

Case 2: If user tries to use the bundle which is part of internal http/https location
```bash
$ crc config set bundle https://<internal_server>/crc_libvirt_4.11.3_amd64.crcbundle
$ crc setup
$ crc start
```

Case 3: If a user tries to use the bundle which is downloaded locally
```bash
$ crc config set bundle <local_bundle_path>
$ crc setup
$ crc start
```

As usual, we'd like to get as much [feedback](https://github.com/code-ready/crc/issues/new/choose) as possible on all this work!
