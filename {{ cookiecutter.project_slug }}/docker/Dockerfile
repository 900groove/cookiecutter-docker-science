{%- if cookiecutter.use_nvidia_docker == 'yes' -%}
FROM nvidia/cuda:8.0-cudnn5-devel-ubuntu16.04
{%- else -%}
FROM python:3.7
{%- endif %}

RUN apt update && apt install -y \
    git \
    make \
    curl \
    wget \
    xz-utils \
    sudo \
    file \
    mecab \
    libmecab-dev \
    mecab-ipadic-utf8

RUN git clone --depth 1 https://github.com/neologd/mecab-ipadic-neologd.git\
    && cd mecab-ipadic-neologd\
    && bin/install-mecab-ipadic-neologd -n -y

COPY ./requirements.txt /requirements.txt
RUN pip install -r /requirements.txt

ARG UID
RUN useradd docker -l -u $UID -s /bin/bash -m
USER docker

WORKDIR /work

ENTRYPOINT ["/bin/bash"]
