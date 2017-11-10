FROM jupyter/scipy-notebook@sha256:3f145cc7967ce5ad157f57653180801e3dd26f4c97afa267870195db6ebcec60

LABEL maintainer="Tyler Erickson <tylere@google.com>"

USER root

RUN apt-get update \
  && apt-get install -y --no-install-recommends \
             libjpeg-dev \
             libgif-dev \
             libcairo2-dev \
             pkg-config \
  && pip install ipywidgets==7.0.3 \
  && jupyter nbextension enable --py --sys-prefix widgetsnbextension  \
  && jupyter labextension install @jupyter-widgets/jupyterlab-manager@0.29.3 \
  && pip install ipyleaflet==0.5.1 \
  && jupyter nbextension enable --py --sys-prefix ipyleaflet \
  && jupyter labextension install jupyter-leaflet@0.5.0 \
  && apt-get install -y --no-install-recommends \
             build-essential \
             libssl-dev \
             libffi-dev \
  && pip install cryptography \
  && apt-get purge -y build-essential \
             libssl-dev \
             libffi-dev \
             dpkg-dev \
             pkg-config \
             fakeroot \
             libfakeroot:amd64 \
  && apt-get autoremove -y \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/*

# Install the Earth Engine Python API.
# This is installed as the last step because the package is updated often.
RUN pip install earthengine-api

USER $NB_USER