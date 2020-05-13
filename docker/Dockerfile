FROM nvidia/cuda:10.2-cudnn7-devel-ubuntu16.04
ARG PYTHON_VERSION=3.7
ARG WITH_TORCHVISION=1
RUN apt-get update && apt-get -y upgrade && apt-get install -y --no-install-recommends \
         build-essential \
         cmake \
         pkg-config \
         libatlas-base-dev \
         gfortran \
         unzip \
         git \
         curl \
         ca-certificates \
         libjpeg-dev \
         software-properties-common \
         libpng-dev && \
    add-apt-repository -y ppa:deadsnakes/ppa && \
    add-apt-repository -y universe && \
    apt-get update && \
    apt-get install -y python$PYTHON_VERSION && \
    ln /usr/bin/python$PYTHON_VERSION /usr/bin/python && \
    rm -rf /var/lib/apt/lists/*

RUN curl -o ~/miniconda.sh https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh && \
     chmod +x ~/miniconda.sh && \
     ~/miniconda.sh -b -p /opt/conda && \
     rm ~/miniconda.sh && \
     /opt/conda/bin/conda install -y numpy pyyaml scipy ipython mkl mkl-include ninja cython typing && \
     /opt/conda/bin/conda install -y -c cpbotha magma-cuda10 && \
     /opt/conda/bin/conda clean -ya && \
     curl "https://bootstrap.pypa.io/get-pip.py" -o "get-pip.py" && python get-pip.py --user

ENV PATH /opt/conda/bin:$PATH

RUN wget https://github.com/opencv/opencv/archive/3.4.0.zip -O opencv-3.4.0.zip && \
    unzip opencv-3.4.0.zip && \

WORKDIR opencv-3.4.0

RUN mkdir build && cd build && \
    cmake -D CMAKE_BUILD_TYPE=RELEASE \
        -D CMAKE_INSTALL_PREFIX=/usr/local \
        -D PYTHON_EXECUTABLE=~/.virtualenvs/r21d/bin/python \
        -D BUILD_EXAMPLES=ON \
	-D BUILD_SHARED_LIBS=ON ..
