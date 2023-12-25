FROM debian:stable-slim

ARG NCS_SDK_VERSION=v2.5.0

# OS dependencies and packages

RUN \
  apt-get -y update \
  && apt-get -y install --no-install-recommends \
  ca-certificates \
  cmake \
  device-tree-compiler \
  git \
  ninja-build \
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
  && nrfutil install toolchain-manager \
  && nrfutil toolchain-manager install --ncs-version ${NCS_SDK_VERSION} \
  && apt-get remove -y --purge \
  wget \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/*

# Python

ENV VIRTUAL_ENV=/opt/venv
RUN \
  apt-get -y update \
  && apt-get -y install --no-install-recommends \
  python3 \
  python3-pip \
  python3-venv \
  && python3 -m venv $VIRTUAL_ENV
ENV PATH="$VIRTUAL_ENV/bin:$PATH"

# West

RUN pip install --no-cache-dir wheel west