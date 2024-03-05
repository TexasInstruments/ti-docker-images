# ti-docker-images

This repository provides a ubuntu 22.04 based docker image with all the packages that are required for Yocto Builds. 
The docker image can also be used to Install & Build via Top Level Makefile from sources for [TI Arm based microprocessors](https://www.ti.com/microcontrollers-mcus-processors/arm-based-processors/products.html)

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
