# jupyterlab-ee
Experiments related to getting JupyterLab and Earth Engine to work together.

![Alt text](/images/Screenshot-2017-09-14.png?raw=true "JupyterLab + Earth Engine")

# Install instructions

    docker build --tag jupyterlab-ee .
    docker run -it -p 8888:8888 --rm jupyterlab-ee:latest start.sh jupyter lab
