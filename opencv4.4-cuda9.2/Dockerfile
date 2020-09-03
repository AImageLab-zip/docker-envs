FROM nvidia/cuda:9.2-devel

WORKDIR /home

# cmake 3.13.4
RUN apt-get update && apt-get install -y wget \
    && wget https://github.com/Kitware/CMake/releases/download/v3.13.4/cmake-3.13.4-Linux-x86_64.sh \
      -q -O /tmp/cmake-install.sh \
    && chmod u+x /tmp/cmake-install.sh \
    && mkdir /home/cmake-3.13.4 \
    && /tmp/cmake-install.sh --skip-license --prefix=/home/cmake-3.13.4 \
    && rm /tmp/cmake-install.sh \
    && update-alternatives --install /usr/bin/cmake cmake /home/cmake-3.13.4/bin/cmake 10 \
    && update-alternatives --install /usr/bin/ctest ctest /home/cmake-3.13.4/bin/ctest 10 \
    && update-alternatives --install /usr/bin/cpack cpack /home/cmake-3.13.4/bin/cpack 10 
    
# opencv 4.4 (and contrib for CUDA)
RUN mkdir opencv \
    && mkdir opencv/contrib \
    && wget -P opencv/ https://github.com/opencv/opencv/archive/4.4.0.tar.gz \
    && wget -P opencv/contrib/ https://github.com/opencv/opencv_contrib/archive/4.4.0.tar.gz \
    && tar -xvzf opencv/4.4.0.tar.gz -C opencv \
    && rm opencv/4.4.0.tar.gz \
    && tar -xvzf opencv/contrib/4.4.0.tar.gz -C opencv/contrib \
    && rm opencv/contrib/4.4.0.tar.gz \
    && cd opencv/opencv-4.4.0 \
    && mkdir gcc5_static_bin_cuda \
    && cd gcc5_static_bin_cuda \
    && cmake \
        -D WITH_CUDA=ON \
        -D BUILD_LIST=core,imgcodecs,imgproc,features2d,cudev,cudaarithm,cudafilters,cudafeatures2d,cudawarping \
        -D BUILD_SHARED_LIBS=OFF \
        -D OPENCV_EXTRA_MODULES_PATH=/home/opencv/contrib/opencv_contrib-4.4.0/modules \
        -D CMAKE_INSTALL_PREFIX=`pwd`/install \
        -D CMAKE_CXX_FLAGS="${CMAKE_CXX_FLAGS} -std=c++14" \
        -D CUDA_NVCC_FLAGS="${CUDA_NVCC_FLAGS} -std=c++14" \
        -D CMAKE_BUILD_TYPE=Release \
        .. \
    && cmake --build . --config Release -- -j7 \
    && cmake --build . --target install

# install tools
RUN apt-get install -y unzip gnuplot