FROM debian:stable-slim

ARG NCS_SDK_VERSION=v2.5.0

# OS dependencies and packages

RUN \
  apt-get -y update \
  && apt-get -y install --no-install-recommends \
  ca-certificates \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/*

# NCS SDK

RUN \
  apt-get -y update \
  && apt-get -y install --no-install-recommends \
  wget \
  && wget https://developer.nordicsemi.com/.pc-tools/nrfutil/x64-linux/nrfutil \
  && chmod +x nrfutil \
  && mv nrfutil /usr/bin \
  && nrfutil install sdk-manager \
  && nrfutil sdk-manager toolchain install --ncs-version ${NCS_SDK_VERSION} \
  && apt-get remove -y --purge \
  wget \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/* \
  && rm -rf ncs/downloads
