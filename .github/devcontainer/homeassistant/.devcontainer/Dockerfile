FROM ghcr.io/uwu/basic-env/base:latest

USER root

ENV \
    DEBIAN_FRONTEND=noninteractive \
    DEVCONTAINER=1

SHELL ["/bin/bash", "-o", "pipefail", "-c"]

# Install tools
RUN \
    apt-get update \
    && apt-get install -y --no-install-recommends \
        dbus \
        network-manager \
        libpulse0 \
        xz-utils

COPY ./common/rootfs /
COPY ./common/rootfs_supervisor /
COPY ./common/install /tmp/common/install

# Install common
RUN bash devcontainer_init
# Is chmod really needed if we're root? It's missing eXecution permissions, but is that really an issue?
#RUN bash chmod 777 /usr/bin/get_arch
RUN bash common_install_packages docker || true
RUN bash common_install_packages docker shellcheck cosign os-agent || true
RUN bash usermod -aG docker coder

COPY ./addons/rootfs /

USER coder
ENV DEBIAN_FRONTEND="dialog"
