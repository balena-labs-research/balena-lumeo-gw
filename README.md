# balena-lumeo-gw
An x86 [Lumeo](https://lumeo.com/) gateway running on [balena](https://www.balena.io/)

Requires a supported NVIDIA gpu. 

## How it works

The gpu container downloads the kernel source file for our exact OS version, builds the NVIDIA modules, and loads them into the host OS. We install the same NVIDIA driver (must be same version as in the gpu container) into the lumeo base image. You must set all the variables listed below and make sure all versions of the NVIDIA driver as well as the kernel source file versions match.

## Setup

Clone this repo to your development device then set the following values:

TBA



This is based on https://github.com/balena-io-examples/nvidia-x86 for running NVIDIA gpus on balena.
