# Using debian:trixie-slim as the base image
FROM arm64v8/debian:trixie-slim
RUN export DEBIAN_FRONTEND=noninteractive
RUN apt-get update ; apt-get -y install net-tools git wget vim sudo zip corkscrew rsync iputils-ping locales apt-utils gpg tzdata devscripts equivs debmake qt6-base-dev qt6-multimedia-dev libqt6quick6 qt6-declarative-dev cmake libgstreamer1.0-dev
RUN locale-gen en_US en_US.UTF-8
RUN echo "dash dash/sh boolean false" | debconf-set-selections && \
    DEBIAN_FRONTEND=noninteractive dpkg-reconfigure dash && \
    export LC_ALL="en_US.UTF-8" && \
    export LC_CTYPE="en_US.UTF-8" && \
    export LC_NUMERIC="en_US.UTF-8"

