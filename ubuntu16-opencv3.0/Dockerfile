FROM ubuntu:16.04

ARG CMAKE_VER=3.13.5
ARG CV_VER=3.0.0
ARG GCC_VER=5

ENV NUM_CORES 4

# Turn off interactive dialogs of dpkg
# https://askubuntu.com/a/1013396/44054
# https://stackoverflow.com/a/44333806/424986
ENV DEBIAN_FRONTEND=noninteractive

#RUN apt-get update \
#    && apt-get install -y gcc-$GCC_VER g++-$GCC_VER gcc-$GCC_VER-multilib g++-$GCC_VER-multilib \
#    && update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-$GCC_VER 10 \
#    && update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-$GCC_VER 10 \
#    && update-alternatives --install /usr/bin/cc cc /usr/bin/gcc 20 \
#    && update-alternatives --set cc /usr/bin/gcc \
#    && update-alternatives --install /usr/bin/c++ c++ /usr/bin/g++ 20 \
#    && update-alternatives --set c++ /usr/bin/g++    
    
RUN apt-get update && apt-get install -y wget \
    && wget https://github.com/Kitware/CMake/releases/download/v$CMAKE_VER/cmake-$CMAKE_VER-Linux-x86_64.sh \
      -q -O /tmp/cmake-install.sh \
    && chmod u+x /tmp/cmake-install.sh \
    && mkdir /home/cmake-$CMAKE_VER \
    && /tmp/cmake-install.sh --skip-license --prefix=/home/cmake-$CMAKE_VER \
    && rm /tmp/cmake-install.sh \
    && update-alternatives --install /usr/bin/cmake cmake /home/cmake-$CMAKE_VER/bin/cmake 10 \
    && update-alternatives --install /usr/bin/ctest ctest /home/cmake-$CMAKE_VER/bin/ctest 10 \
    && update-alternatives --install /usr/bin/cpack cpack /home/cmake-$CMAKE_VER/bin/cpack 10


# Install OpenCV
RUN apt-get -y update -qq && \
    apt-get -y install unzip \
                       \
                       # Required
                       build-essential \
                       # gcc-multilib for 32 bit compilation
                       gcc-multilib \ 
                       g++-multilib \
                       git \
                       pkg-config \
                       #libatlas-base-dev \
                       #libavcodec-dev \
                       #libavformat-dev \
                       #libgtk2.0-dev \
                       #libswscale-dev \
                       \
                       # Optional
#                        libjpeg-dev \
#                        libpng-dev \
#                        libtiff-dev \
                       gnuplot \
                       vim \
                       &&\ 
    apt-get autoclean autoremove

    # Get OpenCV
RUN git clone https://github.com/opencv/opencv.git &&\
    cd opencv &&\
    git checkout $CV_VER &&\
    cd / &&\
    # Get OpenCV contrib modules
    #git clone https://github.com/opencv/opencv_contrib &&\
    #cd opencv_contrib &&\
    #git checkout $CV_VER &&\
    mkdir /opencv/build &&\
    cd /opencv/build &&\
    \
    # Lets build OpenCV
    cmake \
    -D CMAKE_BUILD_TYPE=RELEASE \
    -D CMAKE_INSTALL_PREFIX=/usr/local \
    -D BUILD_DOCS=OFF \
    -D BUILD_EXAMPLES=OFF \
    -D BUILD_JASPER=OFF \
    -D BUILD_JAVA=OFF \
    -D BUILD_JPEG=ON \
    -D BUILD_LIST=core,imgproc,imgcodecs \
    -D BUILD_PERF_TESTS=OFF \
    -D BUILD_PNG=ON \
    -D BUILD_PROTOBUF=OFF \
    -D BUILD_SHARED_LIBS=OFF \
    -D BUILD_TESTS=OFF \
    -D BUILD_TIFF=ON \
    -D BUILD_USE_SYMLINKS=OFF \
    -D BUILD_WEBP=OFF \
    -D BUILD_WITH_DEBUG_INFO=OFF \
    -D BUILD_WITH_DYNAMIC_IPP=OFF \
    -D BUILD_ZLIB=OFF \ 
    -D WITH_FFMPEG=OFF \
    -D WITH_OPENCL=OFF \ 
    -D WITH_QT=OFF \ 
    -D WITH_IPP=OFF \
    -D WITH_MATLAB=OFF \
    -D WITH_OPENGL=OFF \
    -D WITH_QT=OFF \ 
    -D WITH_TIFF=OFF \
    -D WITH_TBB=OFF \
    -D WITH_V4L=OFF \
    -D WITH_LAPACK=OFF \
    -D INSTALL_C_EXAMPLES=OFF \
    -D INSTALL_PYTHON_EXAMPLES=OFF \ 
    -D WITH_OPENEXR=OFF \
    -D CMAKE_CXX_FLAGS=-m32 \
    -D CMAKE_C_FLAGS=-m32 \
    .. &&\
    make -j$NUM_CORES &&\
    make install &&\
    ldconfig &&\
    \
    # Clean the install from sources
    cd / &&\
    rm -r /opencv 

# Change working dirs
WORKDIR /builds

# Define default command.
CMD ["bash"]
