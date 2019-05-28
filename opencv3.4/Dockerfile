FROM stal12/ubuntu18-gcc5

WORKDIR /home

# Installare git, gcc, make e cmake
# Sono nell'immagine padre

# Install opencv-3.4.6 with selected modules
RUN apt-get update && apt-get install -y wget \
    && wget https://github.com/opencv/opencv/archive/3.4.6.tar.gz \
    && tar -xvzf 3.4.6.tar.gz opencv-3.4.6 \
    && rm 3.4.6.tar.gz \
    && cd opencv-3.4.6 \
    && mkdir gcc5.5_static_bin \
    && cd gcc5.5_static_bin \
    && cmake \
        -D BUILD_SHARED_LIBS=OFF \
        -D CMAKE_INSTALL_PREFIX=`pwd`/install \
        -D BUILD_opencv_apps=OFF \
        -D BUILD_opencv_calib3d=OFF \
        -D BUILD_opencv_dnn=OFF \
        -D BUILD_opencv_features2d=OFF \
        -D BUILD_opencv_flann=OFF \
        -D BUILD_opencv_highgui=OFF \
        -D BUILD_opencv_java_bindings_generator=OFF \
        -D BUILD_opencv_js=OFF \
        -D BUILD_opencv_ml=OFF \
        -D BUILD_opencv_objdetect=OFF \
        -D BUILD_opencv_photo=OFF \
        -D BUILD_opencv_python_bindings_generator=OFF \
        -D BUILD_opencv_shape=OFF \
        -D BUILD_opencv_stitching=OFF \
        -D BUILD_opencv_superres=OFF \
        -D BUILD_opencv_ts=OFF \
        -D BUILD_opencv_video=OFF \
        -D BUILD_opencv_videoio=OFF \
        -D BUILD_opencv_videostab=OFF \
        -D BUILD_opencv_world=OFF \
        -D BUILD_opencv_core=ON \
        -D BUILD_opencv_imgcodecs=ON \
        -D BUILD_opencv_imgproc=ON \
        -D CMAKE_BUILD_TYPE=Release \
        .. \
    && cmake --build . -j7 \
    && cmake --build . --target install
    
ENV OpenCV_DIR=/home/opencv-3.4.6/gcc5.5_static_bin
