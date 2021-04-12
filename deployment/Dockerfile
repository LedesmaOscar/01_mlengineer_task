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

# Create a new Python env and include it in the PATH
RUN python3 -m venv /home/venv
ENV PATH="/home/venv/bin:$PATH"

# Creates a new Ubuntu user
RUN useradd -m model-server

# COPY . /

# Expose the ports 8500 (gRPC) and 8501 (REST)
ENV GRPC_PORT=8500
ENV REST_PORT=8501
EXPOSE $GRPC_PORT $REST_PORT


ENTRYPOINT ["/usr/bin/tf_serving_entrypoint.sh"]

RUN mkdir /home/Metro && cd /home/Metro       
WORKDIR /home/Metro

# Creates a directory for the logs and sets permissions to it
RUN mkdir /home/logs 
RUN chown -R model-server /home/logs
       
RUN git clone https://github.com/LedesmaOscar/01_mlengineer_task.git 

# Defines the model_path  variable and the model name
ENV MODEL_BASE_PATH=/home/Metro/01_mlengineer_task
ENV MODEL_NAME=dnn_model

# Prepare the CMD that will be run on docker run
RUN chown -R model-server /home/venv
RUN chown -R model-server /home/Metro
USER model-server
CMD tensorflow_model_server --port=$GRPC_PORT --rest_api_port=$REST_PORT --model_name=$MODEL_NAME --model_base_path=$MODEL_PATH >> /home/logs/server.log


