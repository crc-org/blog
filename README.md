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
$ podman run --rm -v $PWD:/workspace quay.io/crc-org/hugo:0.127.0 --minify
```

This will create a `./public/` folder that contains the output as published on GH Pages.

> [!IMPORTANT]
> Make sure to run `git submodule update --init` to pull remote modules, otherwise the theme will not be available. This will cause the generation to fail


### Devcontainer
You can also use the devcontainer setup. This will start the generation container and allows you to use the `hugo` command line directlky from inside the editor.

This can be started from CodeSpaces, VS Code or the CLI

```
$ npm install -g @devcontainers/cli
$ devconatiner up
```
