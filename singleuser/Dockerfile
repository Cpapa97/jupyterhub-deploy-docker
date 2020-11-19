ARG DOCKER_NOTEBOOK_IMAGE

FROM at-docker.ad.bcm.edu:5000/minnie65p3-stelios:latest as intermediate

FROM $DOCKER_NOTEBOOK_IMAGE
ARG JUPYTERHUB_VERSION

LABEL maintainer="Christos Papadopoulos"

# deal with permission issues temporarily, (supposedly) reset down below
# USER root


###############################################################################

# Install dependency apt packages
RUN apt-get update && \
    apt-get -y install graphviz libxml2 libxml2-dev zlib1g-dev build-essential python-dev \
    python-igraph python3-cairosvg parallel fish python3-pip

RUN python3 -m pip install --upgrade pip

###############################################################################

# Requisite python packages
RUN pip3 install xlrd ipyvolume jupyterlab statsmodels && \
    pip3 install pycircstat nose autograd seaborn jgraph trimesh &&\
    pip3 install importlib --upgrade

###############################################################################

# Jupyterhub
RUN pip3 install jupyterhub==$JUPYTERHUB_VERSION

###############################################################################

# Datajoint
RUN pip3 install datajoint==0.12.3

###############################################################################

# Install most important packages

WORKDIR /src

# Allen institute packages
# RUN git clone -b phase3 --single-branch https://github.com/AllenInstitute/em_coregistration.git
# RUN pip3 install -e /src/em_coregistration

# minnie65p3
# ADD . /src/minnie65p3
# RUN pip3 install -e /src/minnie65p3/python

COPY --from=intermediate /src/em_coregistration .
RUN pip3 install -e /src/em_coregistration

COPY --from=intermediate /src/minnie65p3 .
RUN pip3 install -e /src/minnie65p3/python

# stop running commands as root (supposedly)
# USER 1001

WORKDIR /static-notebooks
COPY --from=builder /src/minnie65p3/notebooks/ .
# COPY /notebooks/* ./
WORKDIR /content