# Using debian:bookworm-slim as the base image
FROM arm64v8/debian:bookworm-slim
RUN export DEBIAN_FRONTEND=noninteractive
RUN apt-get update ; apt-get -y install net-tools git wget vim sudo zip corkscrew rsync iputils-ping locales apt-utils gpg tzdata devscripts equivs debmake
RUN locale-gen en_US en_US.UTF-8
RUN echo "dash dash/sh boolean false" | debconf-set-selections && \
    DEBIAN_FRONTEND=noninteractive dpkg-reconfigure dash && \
    export LC_ALL="en_US.UTF-8" && \
    export LC_CTYPE="en_US.UTF-8" && \
    export LC_NUMERIC="en_US.UTF-8"

