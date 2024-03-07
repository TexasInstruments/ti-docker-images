# Using ubuntu:22.04 as the base image
FROM amd64/ubuntu:22.04

# Installing packages needed for Yocto & SDK Makefile builds
RUN export DEBIAN_FRONTEND=noninteractive; apt-get update && \
         apt-get install -y --no-install-recommends file autoconf automake iproute2 usbutils dialog dfu-util \
         bison flex libssl-dev bc u-boot-tools swig wget device-tree-compiler python3 python3-pip python3-dev dosfstools fdisk sudo && \
         pip3 install jsonschema pyelftools PyYAML Mako && \
         
         apt-get install -y gawk git diffstat unzip texinfo gcc build-essential chrpath socat cpio python3 python3-pip python3-pexpect \
         xz-utils debianutils iputils-ping python3-git python3-jinja2 libegl1-mesa libsdl1.2-dev xterm pylint python3-subunit mesa-common-dev \
         zstd liblz4-tool file locales doxygen dos2unix bison flex libssl-dev u-boot-tools mono-devel mono-complete curl python3-distutils repo \
         pseudo python3-sphinx g++-multilib libc6-dev-i386 jq git-lfs pigz liblz4-tool lz4 net-tools zip corkscrew rsync \
         iputils-ping locales apt-utils nano && locale-gen en_US en_US.UTF-8 && rm -rf /var/lib/apt/lists/*

# Set locale's and reconfigure to use bash as the default shell for /bin/sh.
RUN export DEBIAN_FRONTEND=noninteractive; echo "dash dash/sh boolean false" | debconf-set-selections && \
         dpkg-reconfigure dash && addgroup --gid 786 tisdk && \
         # Add user tisdk with uid & gid as 786.
         adduser --disabled-password --uid 786 --gid 786 --gecos "" --home /home/tisdk --shell /bin/bash tisdk && \
         # Add tisdk to sudoers & make it passwordless
         adduser tisdk sudo && usermod -aG sudo tisdk && echo "tisdk ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers && \
         export LC_ALL="en_US.UTF-8" && export LC_CTYPE="en_US.UTF-8" && export LC_NUMERIC="en_US.UTF-8"

# Set default user as tisdk         
USER tisdk
