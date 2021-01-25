FROM dhealth/eddl-toolkit:v0.8.3a
# eddl-toolkit has opencv, eddl, git, cmake, make

ARG CMAKE_VER=3.13.5

# Install missing requirements
RUN apt update && apt install -y curl libopenslide-dev \
  && wget https://github.com/Kitware/CMake/releases/download/v$CMAKE_VER/cmake-$CMAKE_VER-Linux-x86_64.tar.gz \
  && tar -xzf cmake-$CMAKE_VER-Linux-x86_64.tar.gz \
  && mv cmake-$CMAKE_VER-Linux-x86_64 cmake \
  && export PATH=/cmake/bin:$PATH

WORKDIR /opt
