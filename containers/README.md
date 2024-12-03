Fedora image for Hugo-based generation
======================================


This Fedora container image contains:

  - hugo: https://github.com/gohugoio/hugo  
    The world’s fastest framework for building websites


## Usage instructions
Start the container in the folder that contains your blog source

```bash
$ podman run --rm -v $PWD:/workspace \
    quay.io/crc-org/hugo:0.127.0 --minify
```

This will generate a `public` output.

Or using

```bash
$ podman run --rm -v $PWD:/workspace -p 1313:1313 \
    quay.io/crc-org/hugo:0.127.0 \
    server --bind 0.0.0.0
```
the generated content will be published using the embedded server on http://localhost:1313


## Build container

```bash
$ podman build -t hugo -f Containerfile .
```
