FROM amd64/ubuntu:22.04
RUN export DEBIAN_FRONTEND=noninteractive; apt-get update && \
         apt-get install -y --no-install-recommends file build-essential autoconf automake bison flex libssl-dev bc u-boot-tools swig python3 python3-pip wget device-tree-compiler python3-dev dosfstools fdisk sudo && \
         pip3 install jsonschema pyelftools PyYAML Mako && \
         apt-get -f -y install git diffstat texinfo gawk chrpath socat doxygen dos2unix mono-devel mono-complete curl python3-distutils repo pseudo python3-sphinx \
         g++-multilib libc6-dev-i386 jq git-lfs pigz zstd liblz4-tool cpio file zstd lz4 && \
         rm -rf /var/lib/apt/lists/*
