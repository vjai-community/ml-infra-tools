FROM nvidia/cuda:10.2-cudnn7-devel-ubuntu18.04


RUN echo "deb http://developer.download.nvidia.com/compute/machine-learning/repos/ubuntu1804/x86_64 /" > /etc/apt/sources.list.d/nvidia-ml.list

RUN apt-get update && apt-get install -y --no-install-recommends \
         build-essential \
         cmake \
         git \
         curl \
         ca-certificates \
         libjpeg-dev \
         libpng-dev

RUN apt-get -y update && apt-get install -y g++ gcc gfortran build-essential git libopenblas-dev
RUN  rm -rf /var/lib/apt/lists/*

RUN curl -o ~/miniconda.sh -O  https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh  && \
     chmod +x ~/miniconda.sh && \
     ~/miniconda.sh -b -p /opt/conda
RUN rm ~/miniconda.sh

RUN useradd -ms /bin/bash vjai

WORKDIR /tmp/
ADD ./environment.yml /tmp/environment.yml
RUN /opt/conda/bin/conda env create -f environment.yml

ENV PATH /opt/conda/envs/vjai_paper_coding/bin:$PATH