# Docker pulls the specified image and sets it as the working image
# ARG BASE_IMAGE="ubuntu:20.04"
# FROM ${BASE_IMAGE}

# Pull latest image of tensorflow serving
FROM tensorflow/serving:latest

# Allow log messages to be dumped in the stream (not buffer)
ENV PYTHONUNBUFFERED TRUE

# Install the Ubuntu dependencies and Python 3
RUN apt-get update \
    && apt-get install --no-install-recommends -y \
    python3-dev \
    python3-distutils \
    python3-venv \
    curl  \
    git  \
    wget \
    && rm -rf /var/lib/apt/lists/* \
    && cd /tmp \
    && curl -O https://bootstrap.pypa.io/get-pip.py \
    && python3 get-pip.py \
    && rm get-pip.py

#RUN apt-get install -y git


COPY . /

# Expose ports
# gRPC
EXPOSE 8500

# REST
EXPOSE 8501

ENTRYPOINT ["/usr/bin/tf_serving_entrypoint.sh"]


RUN mkdir /home/Metro && cd /home/Metro       
WORKDIR /home/Metro
       
RUN git clone https://github.com/LedesmaOscar/TestMetro.git 

#Set working directory


