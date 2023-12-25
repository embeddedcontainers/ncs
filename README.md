# NCS Container Images

Develop nRF Connect SDK (NCS) applications using OCI-compatible Docker images.

# Getting container images

## Build images locally

Building images locally ensures you can trust the source of the image, as well as allow you to modify the container image configuration.

### Building with Docker CLI

_Build the image_

```
docker build --build-arg NCS_SDK_VERSION=v2.5.0 -f "./ncs/Dockerfile" -t ncs:2.5.0SDK "./ncs"

```