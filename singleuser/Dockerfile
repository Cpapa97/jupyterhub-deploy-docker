# ARG DOCKER_NOTEBOOK_IMAGE

# # Initial image pull (need to figure out how to get more out the output synced from this to avoid copying it all down below and possibly getting desynced)
# FROM at-docker.ad.bcm.edu:5000/minnie65p3-cpapa97:latest as builder

# FROM $DOCKER_NOTEBOOK_IMAGE
# ARG JUPYTERHUB_VERSION


ARG DOCKER_NOTEBOOK_IMAGE
FROM at-docker.ad.bcm.edu:5000/minnie65p3-cpapa97:latest
ARG JUPYTERHUB_VERSION

RUN pip3 install jupyterhub==$JUPYTERHUB_VERSION

WORKDIR /content/notebooks