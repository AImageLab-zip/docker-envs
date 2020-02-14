FROM ubuntu:18.04

# Install gcc-5
RUN apt-get update \
    && apt-get install gcc-5 g++-5 -y \
    && update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-5 10 \
    && update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-5 10 \
    && update-alternatives --install /usr/bin/cc cc /usr/bin/gcc 20 \
    && update-alternatives --set cc /usr/bin/gcc \
    && update-alternatives --install /usr/bin/c++ c++ /usr/bin/g++ 20 \
    && update-alternatives --set c++ /usr/bin/g++    
    
RUN apt-get update && apt-get install -y wget \
    && wget https://github.com/Kitware/CMake/releases/download/v3.14.3/cmake-3.14.3-Linux-x86_64.sh \
      -q -O /tmp/cmake-install.sh \
    && chmod u+x /tmp/cmake-install.sh \
    && mkdir /home/cmake-3.14.3 \
    && /tmp/cmake-install.sh --skip-license --prefix=/home/cmake-3.14.3 \
    && rm /tmp/cmake-install.sh \
    && update-alternatives --install /usr/bin/cmake cmake /home/cmake-3.14.3/bin/cmake 10 \
    && update-alternatives --install /usr/bin/ctest ctest /home/cmake-3.14.3/bin/ctest 10 \
    && update-alternatives --install /usr/bin/cpack cpack /home/cmake-3.14.3/bin/cpack 10 \
    && apt-get remove -y wget \
    && apt-get install libprotobuf8 libprotobuf-c0 libprotoc8
    
RUN apt-get install -y make git
