# docker build -t lfpy:latest .
FROM ubuntu:20.10

LABEL maintainer "An-Cheng Yang<acyang0903@gmail.com>"

ENV LANG=C.UTF-8 LC_ALL=C.UTF-8
ENV PATH /opt/conda/bin:$PATH

RUN apt-get update --fix-missing && \
    apt-get install -y wget bzip2 ca-certificates curl git apt-utils gnupg orca vim vtk && \
    curl https://repo.anaconda.com/pkgs/misc/gpgkeys/anaconda.asc | gpg --dearmor > /tmp/conda.gpg && \
    install -o root -g root -m 644 /tmp/conda.gpg /etc/apt/trusted.gpg.d/ && \
    echo "deb [arch=amd64] https://repo.anaconda.com/pkgs/misc/debrepo/conda stable main" > /etc/apt/sources.list.d/conda.list && \
    apt-get update --fix-missing && \
    apt-get install -y conda && apt-get clean && rm -rf /var/lib/apt/lists/* && \
    ln -s /opt/conda/etc/profile.d/conda.sh /etc/profile.d/conda.sh

RUN conda config --add channels conda-forge && \
    conda create -n lfpy python=3 neuron lfpy ipython jupyterlab git matplotlib make gxx_linux-64 "nodejs>15" ipyparallel plotly psutil requests ipywidgets pandas seaborn vtk && \
    /opt/conda/envs/lfpy/bin/jupyter-lab --generate-config && \
#    sed -ie "s/#c.NotebookApp.tornado_settings = {}/c.NotebookApp.tornado_settings = {'headers':{'Content-Security-Policy':\"frame-ancestors http:\/\/*.*.*.* 'self'\"}}/g" /root/.jupyter/jupyter_notebook_config.py && \
    git clone https://github.com/LFPy/LFPy.git /root/LFPy

RUN conda run -n lfpy jupyter labextension install jupyterlab-plotly @jupyter-widgets/jupyterlab-manager plotlywidget

ENV PATH /opt/conda/envs/lfpy/bin:$PATH

COPY jupyter_notebook_config.py /root/.jupyter/
