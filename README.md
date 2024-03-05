# ti-docker-images

This repository provides a ubuntu 22.04 based docker image with all the packages that are required for Yocto Builds. 
The docker image can also be used to Install & Build via Top Level Makefile from sources for [TI Arm based microprocessors](https://www.ti.com/microcontrollers-mcus-processors/arm-based-processors/products.html)

## Pre-Requisites

First you need to install and setup [docker](https://www.docker.com/). Docker is a software container platform that you need to install on the build host. Depending on your build host, you might have to install different software to support Docker containers. Go to the Docker installation page and read about the platform requirements in [Supported Platforms](https://docs.docker.com/engine/install/#supported-platforms) your build host needs to run containers.

- [Linux Instructions](https://docs.docker.com/engine/install/)
  - [Install Docker Engine for Ubuntu](https://docs.docker.com/engine/install/ubuntu/) for Linux build hosts running the Ubuntu distribution.
  - [Install Docker Engine on CentOS](https://docs.docker.com/engine/install/centos/) for Linux build hosts running the CentOS distribution.
- [Mac Instructions](https://github.com/crops/docker-win-mac-docs/wiki/Mac-Instructions)
- [Windows Instructions](https://github.com/crops/docker-win-mac-docs/wiki/Windows-Instructions-%28Docker-Toolbox%29)

If you are unfamiliar with Docker and the container concept, you can learn more here - https://docs.docker.com/get-started/.

Once you have the setup ready, you should be able to launch Docker or the Docker Toolbox and have a terminal shell on your development host.

## Steps to Run Yocto builds inside Container

### 1. Pulls the Docker Image & Starts a Container

```sh
# On Host
host# export WORK_DIR=<path-to-your-host-where-you-want-to-start-yocto-build>
host# docker run --privileged -it -v ${WORK_DIR}:/home/tisdk -v /dev:/dev -v /media/:/media/ -w /home/tisdk ghcr.io/cshilwant/ubuntu-distro:latest
 
# Inside Container Now
tisdk@9b297a000db9~$ 
tisdk@9b297a000db9:~$ pwd
/home/tisdk
```

> #### 📝 If working behind a proxy, ensure [to setup the network proxy](https://wiki.yoctoproject.org/wiki/Working_Behind_a_Network_Proxy)

### 2. Start Yocto Build


```sh
tisdk@9b297a000db9:~$ pwd
/home/tisdk
 
# Clone oe-layersetup
tisdk@9b297a000db9:~$ git clone https://git.ti.com/git/arago-project/oe-layersetup.git tisdk
tisdk@9b297a000db9:~$ cd tisdk
tisdk@9b297a000db9:~$ ./oe-layertool-setup.sh -f configs/processor-sdk/<oe-config-file>
tisdk@9b297a000db9:~$ cd build  
tisdk@9b297a000db9:~$ . conf/setenv
 
# To build <target> image
tisdk@9b297a000db9:~$ MACHINE=<machine> bitbake -k <target>

# To build tisdk-default-image image for AM62x
tisdk@9b297a000db9:~$ MACHINE=am62xx-evm bitbake -k tisdk-default-image

```

Refer [Build Options under Processor SDK Build Reference](https://software-dl.ti.com/processor-sdk-linux/esd/AM62X/latest/exports/docs/linux/Overview_Building_the_SDK.html#build-options) for machine & target options.

Your `target` wic image will be generated in deploy-ti directory. Refer [Create SD Card](https://software-dl.ti.com/processor-sdk-linux/esd/AM62X/latest/exports/docs/linux/Overview/Processor_SDK_Linux_create_SD_card.html) to flash this image on the SD-Card.
