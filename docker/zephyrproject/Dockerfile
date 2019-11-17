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
RUN apt-get install --no-install-recommends -y \
  git cmake ninja-build gperf \
  ccache dfu-util device-tree-compiler wget \
  xz-utils file \
  make gcc gcc-multilib cmake

SHELL ["/bin/bash", "-c"]

RUN DEBIAN_FRONTEND=noninteractive apt-get install --no-install-recommends -y \
  python3-pip python3-setuptools python3-tk python3-wheel

RUN pip3 install -U west

WORKDIR /root
RUN west init zephyrproject && \
  cd zephyrproject && \
  west update

RUN pip3 install -r ~/zephyrproject/zephyr/scripts/requirements.txt

RUN wget https://github.com/zephyrproject-rtos/sdk-ng/releases/download/v0.10.3/zephyr-sdk-0.10.3-setup.run && \
  chmod +x zephyr-sdk-0.10.3-setup.run && \
  ./zephyr-sdk-0.10.3-setup.run -- -d ~/zephyr-sdk-0.10.3 && \
  rm zephyr-sdk-0.10.3-setup.run

ENV ZEPHYR_TOOLCHAIN_VARIANT=zephyr
ENV ZEPHYR_SDK_INSTALL_DIR=~/zephyr-sdk-0.10.3

