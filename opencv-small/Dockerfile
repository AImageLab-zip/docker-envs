FROM aimagelab/base:latest

ARG CV_VER=4.5.2

ENV NUM_CORES=2

WORKDIR /

# Install OpenCV
RUN wget -q --show-progress --progress=bar:force https://github.com/opencv/opencv/archive/${CV_VER}.tar.gz \
    && tar -xzf ${CV_VER}.tar.gz \
    && rm ${CV_VER}.tar.gz \
    && cd opencv-${CV_VER} \
    && mkdir -p build \
    && cd build \
    \
    && cmake \
    -DCMAKE_BUILD_TYPE=Release \
    -DBUILD_LIST=core,imgproc,imgcodecs,photo,calib3d \
    -DBUILD_opencv_apps=OFF \
    -DBUILD_opencv_java_bindings_generator=OFF \
    -DBUILD_opencv_python3=OFF \
    -DBUILD_opencv_python_bindings_generator=OFF \
    -DBUILD_opencv_python_tests=OFF \
    -DBUILD_EXAMPLES=OFF \
    -DBUILD_DOCS=OFF \
    -DBUILD_JAVA=OFF \
    -DBUILD_JPEG=ON \
    -DBUILD_IPP_IW=OFF \
    -DBUILD_ITT=OFF \
    -DBUILD_PERF_TESTS=OFF \
    -DBUILD_PNG=ON \
    -DBUILD_SHARED_LIBS=OFF \
    -DBUILD_TESTS=OFF \
    -DBUILD_TIFF=ON \
    -DBUILD_WEBP=OFF \
    -DBUILD_ZLIB=OFF \
    -DINSTALL_C_EXAMPLES=OFF \
    -DINSTALL_PYTHON_EXAMPLES=OFF \
    -DWITH_EIGEN=OFF \
    -DWITH_FFMPEG=OFF \
    -DWITH_IPP=OFF \
    -DWITH_ITT=OFF \
    -DWITH_JPEG=ON \
    -DWITH_LAPACK=OFF \
    -DWITH_MATLAB=OFF \
    -DWITH_OPENCL=OFF \
    -DWITH_OPENEXR=OFF \
    -DWITH_OPENGL=OFF \
    -DWITH_PNG=ON \
    -DWITH_PROTOBUF=OFF \
    -DWITH_QUIRC=OFF \
    -DWITH_QT=OFF \
    -DWITH_TBB=OFF \
    -DWITH_TIFF=ON \
    -DWITH_V4L=OFF \
    -DWITH_WEBP=OFF \
    .. \
    && cmake --build . --config Release --parallel $NUM_CORES \
    && cmake --build . --config Release --target install \
    && ldconfig \
    \
    && cd / \
    && rm -rf /opencv-$CV_VER

# Change working dirs
WORKDIR /builds

# Define default command.
CMD ["bash"]