CRC Blog
--------


This is the source of the CRC blog. Content is written in markdown files and the output is generated using Hugo.


## Usage instructions
There are different ways to build the output on this repository.

### Build using container
The simplest way to generate the output is as follows:

```bash
$ git clone https://github.com/crc-org/blog
$ cd blog
$ git submodule update --init
$ podman run --rm -v $PWD:/workspace ghcr.io/gbraad-redhat/hugo:0.127.0 --minify
```
