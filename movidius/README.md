# Intel Movidius Neural Compute Stick

There are two models:

1. Intel Movidius Neural Compute Stick (NCS) is a tiny fanless deep learning USB drive designed to learn AI programming. The NCS is powered by the low power high performance Movidius™ Visual Processing Unit (VPU). The VPU can be found in millions of smart security cameras, gesture controlled drones, industrial machine vision equipment, etc. 

2. Intel Neural Compute Stick 2 is powered by the Intel Movidius X VPU to deliver industry leading performance, wattage, and power. The NEURAL COMPUTE supports OpenVINO, a toolkit that accelerates solution development and streamlines deployment. The Neural Compute Stick 2 offers plug-and-play simplicity, support for common frameworks and out-of-the-box sample applications. Use any platform with a USB port to prototype and operate without cloud compute dependence. The Intel NCS 2 delivers 4 trillion operations per second with 8X performance boost over previous generations.

I own the first model, so all the information in this repository is about the first model.

## Identifying the device

Once the Movidius Compute Stick is plugged:

```
# lsusb
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 005: ID 5986:0706 Acer, Inc Integrated Camera
Bus 001 Device 008: ID 03e7:2150 Intel Myriad VPU [Movidius Neural Compute Stick]
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
# 
```
