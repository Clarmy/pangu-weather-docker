# 使用 NVIDIA CUDA 镜像作为基础
FROM nvidia/cuda:11.6.2-cudnn8-runtime-ubuntu20.04

# 删除默认 Python 环境
RUN apt-get purge -y python* && apt-get autoremove -y && apt-get clean

# 设置非交互式环境变量
ENV DEBIAN_FRONTEND=noninteractive

# 预设一个默认的时区
RUN echo "Asia/Shanghai" > /etc/timezone

# 安装 Python 3.11
RUN apt-get update
RUN apt-get install -y software-properties-common
RUN add-apt-repository ppa:deadsnakes/ppa
RUN apt-get update
RUN apt-get install -y --fix-missing python3.11 python3.11-distutils vim wget curl unzip

# 为 Python3.11 安装 pip
RUN wget https://bootstrap.pypa.io/get-pip.py \
    && python3.11 get-pip.py \
    && rm get-pip.py

# 清理和整理
RUN apt-get autoremove -y && apt-get clean && rm -rf /var/lib/apt/lists/*

# 将 Python3.11 设为默认 Python 环境
RUN update-alternatives --install /usr/bin/python python /usr/bin/python3.11 1

# 安装盘古需要的依赖
RUN pip install -i https://mirrors.aliyun.com/pypi/simple/ onnxruntime-gpu onnx numpy 

# 设置工作目录
WORKDIR /opt

COPY ./models ./models
COPY ./input_data ./input_data
COPY ./sample.py .
