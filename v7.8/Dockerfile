# Start with a base Ubuntu image
FROM ubuntu:18.04

# Install packages required for NEURON and IV compilation
RUN apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get -y install mpich
RUN DEBIAN_FRONTEND=noninteractive apt-get -y install curl

# Install miniconda with python 3.7
RUN curl -o miniconda.sh https://repo.anaconda.com/miniconda/Miniconda3-4.7.12.1-Linux-x86_64.sh
RUN bash miniconda.sh -p /miniconda -b
RUN rm miniconda.sh
ENV PATH=/miniconda/bin:${PATH}

# Create Python 3 environment named 'p3'
RUN conda create -n p3 -c anaconda python=3
ENV PATH /opt/conda/envs/p3/bin:$PATH
RUN /bin/bash -c "source activate p3"

#RUN pip install --upgrade pip
RUN pip install mpi4py NEURON==7.8.0.127

# Remove packages that are not needed to run NEURON
RUN apt -y autoremove --purge
RUN conda clean --all -y
