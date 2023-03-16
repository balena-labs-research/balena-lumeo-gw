# balena-lumeo-gw
An x86 [Lumeo](https://lumeo.com/) gateway running on [balena](https://www.balena.io/)

Requires a supported NVIDIA gpu. 

## How it works

The gpu container downloads the kernel source file for our exact OS version, builds the NVIDIA modules, and loads them into the host OS. We install the same NVIDIA driver (must be same version as in the gpu container) into the lumeo base image. You must set all the variables listed below and make sure all versions of the NVIDIA driver as well as the kernel source file versions match.

## Setup

Clone this repo to your development device then set the following values:

### gpu container settings

- `VERSION` is the version of balenaOS being used on your device. This needs to be URL-encoded, so a plus sign (+) if present needs to be written as `%2B`.

- `BALENA_MACHINE_NAME` is the device type of your balenaOS from [this list](https://docs.balena.io/reference/hardware/devices/)

- set the `YOCTO_VERSION` to the version of Yocto Linux used to build your version of balenaOS. You can find it by logging into your host OS and typing: `uname -r` - in our example, we used balenaOS 2.113.4

### settings in both containers

- `NVIDIA_DRIVER_VERSION` is the version of the Nvidia driver to download and build using [the list found here](https://www.nvidia.com/en-us/drivers/unix/) It needs to be compatible with the version in the underlying Lumeo base image, and must be the same in both the lumeo and gpu containers.

If everything is set up properly, you should see the output below (for your gpu model) in the terminal:

+-----------------------------------------------------------------------------+
| NVIDIA-SMI 470.86       Driver Version: 470.86       CUDA Version: 11.4     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|                               |                      |               MIG M. |
|===============================+======================+======================|
|   0  Quadro P400         Off  | 00000000:01:00.0 Off |                  N/A |
| 22%   37C    P0    N/A /  N/A |      0MiB /  2000MiB |      0%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+
                                                                               
+-----------------------------------------------------------------------------+
| Processes:                                                                  |
|  GPU   GI   CI        PID   Type   Process name                  GPU Memory |
|        ID   ID                                                   Usage      |
|=============================================================================|
|  No running processes found                                                 |
+-----------------------------------------------------------------------------+ 

This is based on https://github.com/balena-io-examples/nvidia-x86 for running NVIDIA gpus on balena.
