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
  && nrfutil install toolchain-manager \
  && nrfutil toolchain-manager install --ncs-version ${NCS_SDK_VERSION} \
  && apt-get remove -y --purge \
  wget \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/* \
  && rm -rf ncs/downloads

WORKDIR /workdir

# Prepare image with a ready to use build environment
SHELL ["nrfutil","toolchain-manager","launch","/bin/bash","--","-c"]
RUN <<EOT
    west init -m https://github.com/nrfconnect/sdk-nrf --mr ${NCS_SDK_VERSION} .
    if [[ $NCS_VERSION =~ "^[a-fA-F0-9]{32}$" ]]; then
        git checkout ${NCS_SDK_VERSION};
    fi
    west update --narrow -o=--depth=1
EOT

# Launch into build environment with the passed arguments
# Currently this is not supported in GitHub Actions
# See https://github.com/actions/runner/issues/1964
ENTRYPOINT [ "nrfutil", "toolchain-manager", "launch", "/bin/bash", "--", "/root/entry.sh" ]
COPY ./entry.sh /root/entry.sh
