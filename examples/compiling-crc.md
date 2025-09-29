---
jupyter:
  jupytext:
    formats: ipynb,md
    text_representation:
      extension: .md
      format_name: markdown
      format_version: '1.3'
      jupytext_version: 1.17.3
  kernelspec:
    display_name: Python 3 (ipykernel)
    language: python
    name: python3
---

# Compiling `crc` using a notebook

This is just an insightful gist that shows how I automate some tasks.



## Setup host

this step prepares the host machine with `podman` and my dotfiles. The dotfiles contains several helper functions that simplify starting the containers.

```bash
apt-get install -y podman
curl -fsSL https://dotfiles.gbraad.nl/install.sh | sh
```

To simplify executing cells with these dotfiles, we can load an extensin that sources the helper functions.

```python
import sys, os
sys.path.append(os.path.expanduser("~/.dotfiles/ipython/.ipython/extensions"))
ip = get_ipython()
ip.extension_manager.load_extension("dotfiles")
```

## Prepare work directory

The source will be stored on the host machine in `~/Projects/crc-org/crc`. To contribute, it is expected your `ssh`-public key is registered with GitHub.

```python
%%dotscript
mkdir -p ~/Projects/crc-org
cd ~/Projects/crc-org
#git clone git@github.com:/crc-org/crc
git clone https://github.com/crc-org/crc
```

## Prepare developer environment

`devenv` is a helper function that starts developer environments using containers that are prepared, published to a public container registry.

The container here is a named `gofedora`, whose source and image is published to https://github.com/gbraad-devenv/fedora-golang, and `ghcr.io/gbraad-devenv/fedora-golang:latest`

The command `noinit` starts this image with `sleep infinity` to ensure the image remains active. Alternatively `system` can be used, which starts this image with `systemd`.

```python
%devenv gofedora rm
```

```python
%devenv gofedora noinit
```

## Compilation

The actual compilation process is performed from the container that was set up in the previous step. It performs a `make clean` and `make`. The host machine will not store any intermediate files, only the result.

```python
%devenv gofedora exec su gbraad -l -c "cd ~/Projects/crc-org/crc && make clean && make cross"
```

```python
%%dotscript
cd ~/Projects/crc-org/crc
git pull
```

```python
%%dotscript
cd ~/Projects/crc-org/crc
out/linux-amd64/crc version
cp -r out/* ~/Uploads/
```

