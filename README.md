A Docker image with [ROS](http://www.ros.org/) and [Intel SGX](https://software.intel.com/en-us/sgx) [SDK and PSW](https://github.com/01org/linux-sgx) (platform software, i.e., runtime) installed.

The version of installed ROS is Kinetic and that of SGX SDK is 1.9. Tested on a host Linux of Ubuntu 14.04.

# How to use

## Prerequisites

Intel SGX [kernel module](https://github.com/01org/linux-sgx-driver) has to be installed and loaded on the host OS kernel.

## Launch

To launch a container of this image, use a Docker command like the following:

```
docker run --device /dev/isgx --device /dev/mei0 --name <your-container-name> tatetian/ros-sgx /sbin/my_init -- <your commmand>
```

For example, to open an interative shell, run:

```
docker run -it --device /dev/isgx --device /dev/mei0 --name test-ros-sgx tatetian/ros-sgx /sbin/my_init -- /bin/bash
```

# Technical details

## ROS

ROS is installed at `/opt/ros/$ROS_DISTRO/` ()

The ROS part of this Dockerfile is essentially the same as the [official ROS Dockerfile](https://hub.docker.com/\_/ros) kinetic-perception.

## Intel SGX

SGX SDK is installed under `/opt/intel/sgxsdk`. You should do:

The SGX part of this Dockerfile is modified from [tozd/sgx Docker image](https://hub.docker.com/r/tozd/sgx).

## Base image

The base image used by this Dockerfile is [phusion/baseimage](https://hub.docker.com/r/phusion/baseimage), which is a more docker-friendly Ubuntu image. For our purpose, the most valuable feature of this base image is its integration of [runit](http://smarden.org/runit), which starts the services required by SGX on the launch of the image.

## Known Issues

 1. Currently, only one running container of this image is allowed since /dev/mei0 can only be used exclusively by a single system service.
