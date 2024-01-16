FROM amd64/ubuntu:22.04
RUN export DEBIAN_FRONTEND=noninteractive; apt-get update && \
         apt-get install -y --no-install-recommends file build-essential autoconf automake bison flex libssl-dev bc u-boot-tools swig python3 python3-pip wget device-tree-compiler python3-dev dosfstools fdisk && \
         pip3 install jsonschema pyelftools PyYAML Mako && \
         rm -rf /var/lib/apt/lists/*
