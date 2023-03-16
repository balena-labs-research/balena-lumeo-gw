FROM lumeo/gateway-nvidia-dgpu:latest

# default user in base image is not root, so change here:
USER root

# Adding to the Lumeo base image above

ENV DEBIAN_FRONTEND noninteractive

# Set variables for the Yocto version of the OS
ENV YOCTO_VERSION=5.15.54
ENV YOCTO_KERNEL=${YOCTO_VERSION}-yocto-standard

# Set variables to download proper NVIDIA driver
ENV NVIDIA_DRIVER_VERSION=525.85.05
ENV NVIDIA_DRIVER=NVIDIA-Linux-x86_64-${NVIDIA_DRIVER_VERSION}

# Install some prereqs
RUN apt-get update && \
    apt-get install -y git wget unzip build-essential libelf-dev bc libssl-dev bison flex software-properties-common libglvnd-dev kmod

WORKDIR /usr/src/nvidia

# Download and compile NVIDIA driver
RUN \
    curl -fsSL -O https://us.download.nvidia.com/XFree86/Linux-x86_64/$NVIDIA_DRIVER_VERSION/$NVIDIA_DRIVER.run && \
    chmod +x ./${NVIDIA_DRIVER}.run && \
    ./${NVIDIA_DRIVER}.run --extract-only && \
    ./${NVIDIA_DRIVER}/nvidia-installer \
    --ui=none \
    --no-questions \
    --no-drm \
    --no-x-check \
    --no-systemd \
    --no-kernel-module \
    --no-distro-scripts \
    --install-compat32-libs \
    --no-nouveau-check \
    --no-rpms \
    --no-backup \
    --no-abi-note \
    --no-check-for-alternate-installs \
    --no-libglx-indirect \
    --install-libglvnd \
    --x-prefix=/tmp/null \
    --x-module-path=/tmp/null \
    --x-library-path=/tmp/null \
    --x-sysconfig-path=/tmp/null \
    --skip-depmod \
    --expert 
