FROM jupyter/scipy-notebook

MAINTAINER Tyler Erickson <tylere@google.com>

USER root

# Install dependencies.
RUN apt-get update \
  # Install ipywidgets. 
  && apt-get install -y --no-install-recommends \
             # For cairo/ipywidgets: 
             libjpeg-dev \
             libgif-dev \
             libcairo2-dev \
             pkg-config \
  && pip install ipywidgets \
  && jupyter nbextension enable --py widgetsnbextension --sys-prefix \
  && jupyter labextension install @jupyter-widgets/jupyterlab-manager \
  # Install ipyleaflet.
  && pip install ipyleaflet \
  && jupyter nbextension enable --py --sys-prefix ipyleaflet \
  # Install Earth Engine dependencies.
  && apt-get install -y --no-install-recommends \
             build-essential \
             libssl-dev \
             libffi-dev \
  && pip install cryptography \
  # Clean up.
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

# Install the JupyterLab extension for ipyleaflet (currently not available on npm)
RUN git clone https://github.com/ellisonbg/ipyleaflet.git
RUN jupyter labextension install ipyleaflet/jslab

# Install the Earth Engine Python API.
# This is installed as the last step because the package is updated often.
RUN pip install earthengine-api

USER $NB_USER