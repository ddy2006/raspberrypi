FROM balenalib/raspberry-pi-debian:buster-build-20210812 AS builder

RUN echo deb https://mirrors.tuna.tsinghua.edu.cn/raspbian/raspbian/ buster main contrib non-free rpi  > /etc/apt/sources.list \
  && echo deb-src https://mirrors.tuna.tsinghua.edu.cn/raspbian/raspbian/ buster main contrib non-free rpi >> /etc/apt/sources.list \
  && echo deb https://mirrors.tuna.tsinghua.edu.cn/raspberrypi/ buster main ui > /etc/apt/sources.list.d/raspi.list

RUN apt-get update \
    && apt-get upgrade 
RUN apt-get install -y --fix-missing \
    build-essential \
    cmake \
    gfortran \
    git \
    wget \
    curl \
    graphicsmagick \
    libgraphicsmagick1-dev \
    libatlas-base-dev \
    libavcodec-dev \
    libavformat-dev \
    libgtk2.0-dev \
    libjpeg-dev \
    liblapack-dev \
    libswscale-dev \
    pkg-config \
    python3-dev \
    python3-numpy \
    software-properties-common \
    zip \
    && apt-get clean && rm -rf /tmp/* /var/tmp/*

# Virtual Environment
ENV VIRTUAL_ENV=/opt/venv
RUN apt-get update && apt-get install -y python3-venv python3-pip
ENV PATH="$VIRTUAL_ENV/bin:$PATH"

# Install Dlib
ENV CFLAGS=-static
RUN pip3 install --upgrade pip && pip3 install setuptools 
RUN pip3 install numpy
RUN pip3 install dlib

# RUN     git clone -b 'v19.21' --single-branch https://github.com/davisking/dlib.git && \
#     cd dlib/ && \
#     python3 setup.py install --set BUILD_SHARED_LIBS=OFF

RUN pip3 install face_recognition

# FROM balenalib/raspberry-pi-debian:buster-run-20210812
