FROM nvidia/cuda:10.1-devel-ubuntu18.04

ARG GCC_VER=7
ARG CMAKE_VER=3.17.2

ENV TZ=Europe/Rome
ENV NUM_CORES 4

# Prevent user input waiting
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# Turn off interactive dialogs of dpkg
# https://askubuntu.com/a/1013396/44054
# https://stackoverflow.com/a/44333806/424986
ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update \
    && apt-get install -y gcc-$GCC_VER g++-$GCC_VER gcc-$GCC_VER-base \
    && update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-$GCC_VER 100 \
    && update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-$GCC_VER 100

RUN apt-get install -y make wget git graphviz

RUN wget https://github.com/Kitware/CMake/releases/download/v$CMAKE_VER/cmake-$CMAKE_VER-Linux-x86_64.sh \
      -q -O /tmp/cmake-install.sh \
    && chmod u+x /tmp/cmake-install.sh \
    && mkdir /cmake-$CMAKE_VER \
    && /tmp/cmake-install.sh --skip-license --prefix=/cmake-$CMAKE_VER \
    && rm /tmp/cmake-install.sh \
    && update-alternatives --install /usr/bin/cmake cmake /cmake-$CMAKE_VER/bin/cmake 100 \
    && update-alternatives --install /usr/bin/ctest ctest /cmake-$CMAKE_VER/bin/ctest 100 \
    && update-alternatives --install /usr/bin/cpack cpack /cmake-$CMAKE_VER/bin/cpack 100


# Change working dirs
WORKDIR /builds

# Define default command
CMD ["bash"]