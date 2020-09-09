# docker build -t "nvidia/cuda:10.1-cudnn7-devel-ubuntu18.04" .
#

#FROM nvidia/cuda:10.1-cudnn7-devel-ubuntu18.04

FROM ubuntu:20.10

LABEL maintainer "An-Cheng Yang<acyang0903@gmail.com>"

ENV LANG=C.UTF-8 LC_ALL=C.UTF-8
ENV PATH /opt/conda/bin:$PATH

RUN apt-get update --fix-missing && \
    apt-get install -y wget bzip2 ca-certificates curl git apt-utils gnupg orca vim && \
    wget https://neuron.yale.edu/ftp/neuron/versions/v7.7/nrn-7.7.x86_64-linux.deb && \
    dpkg -i nrn-7.7.x86_64-linux.deb && \
    curl https://repo.anaconda.com/pkgs/misc/gpgkeys/anaconda.asc | gpg --dearmor > /tmp/conda.gpg && \
    install -o root -g root -m 644 /tmp/conda.gpg /etc/apt/trusted.gpg.d/ && \
    echo "deb [arch=amd64] https://repo.anaconda.com/pkgs/misc/debrepo/conda stable main" > /etc/apt/sources.list.d/conda.list && \
    ln -s /opt/conda/etc/profile.d/conda.sh /etc/profile.d/conda.sh && \
    echo ". /opt/conda/etc/profile.d/conda.sh" >> ~/.bashrc && \
    echo "conda activate base" >> ~/.bashrc && \
    apt-get update --fix-missing && \
    apt-get install -y conda && apt-get clean && rm -rf /var/lib/apt/lists/*

RUN conda config --add channels conda-forge && \
    conda create -n lfpy python=3.7 lfpy ipython jupyterlab git matplotlib make gxx_linux-64 nodejs ipyparallel plotly psutil requests && \
    echo "source activate lfpy" > ~/.bashrc && \
    git clone https://github.com/LFPy/LFPy.git /opt/LFPy && \
    /opt/conda/envs/lfpy/bin/jupyter-lab --generate-config

ENV PATH /opt/conda/envs/lfpy/bin:$PATH

COPY jupyter_notebook_config.py /root/.jupyter/
