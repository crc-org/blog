CRC Blog
--------


## Build
```shell
$ git clone https://github.com/crc-org/blog
$ cd blog
$ git submodule update
$ podman run --rm -v $PWD:/workspace ghcr.io/gbraad-redhat/hugo:0.127.0 --minify
```