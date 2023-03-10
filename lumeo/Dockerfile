FROM lumeo/gateway-nvidia-dgpu:latest

# Starting with the Lumeo base image above

ENV DEBIAN_FRONTEND noninteractive

# Install Nvidia driver. Must match version in gpu container exactly
RUN \
    apt-get update && \
    apt install -y software-properties-common && \
    add-apt-repository ppa:graphics-drivers/ppa && \
    apt update && \
    apt install -y nvidia-driver-525
    
