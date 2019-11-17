FROM ubuntu:18.04 AS base

# Cmake 3.13.1
RUN apt-get update && \
  apt-get upgrade -y

RUN apt-get install --no-install-recommends -y \
  gnupg gnupg1 gnupg2 \
  ca-certificates wget \
  software-properties-common
RUN wget -O - https://apt.kitware.com/keys/kitware-archive-latest.asc | apt-key add -
RUN add-apt-repository 'deb https://apt.kitware.com/ubuntu/ bionic main'

# Zephyr - install dependencies
# I'm skipping python3 on purpose, we are going to use miniconda
RUN apt-get install --no-install-recommends -y \
  git cmake ninja-build gperf \
  ccache dfu-util device-tree-compiler wget \
  xz-utils file \
  make gcc gcc-multilib cmake


