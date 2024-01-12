ARG BASE_DISTRO=amd64/debian:stable-slim
FROM $BASE_DISTRO
LABEL org.opencontainers.image.source https://github.com/cshilwant/docker-images/ubuntu
RUN export DEBIAN_FRONTEND=noninteractive; apt-get update
RUN export DEBIAN_FRONTEND=noninteractive; \
         apt-get install -y --no-install-recommends file build-essential autoconf automake bison flex libssl-dev bc u-boot-tools swig python3 python3-pip wget nano
