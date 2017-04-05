# Builds a Docker image for Octave with Jupyter Notebook.
#
# It can be found at:
#   https://hub.docker.com/r/compdatasci/octave-notebook
#
# Authors:
# Xiangmin Jiao <xmjiao@gmail.com>

FROM compdatasci/base
LABEL maintainer "Xiangmin Jiao <xmjiao@gmail.com>"

USER root
WORKDIR /tmp

# Install octave, octave_kernel, liboctave-dev, symbolic and odepkg
RUN apt-add-repository ppa:octave/stable && \
    apt-get update && \
    apt-get install -y --no-install-recommends \
        build-essential make \
        octave liboctave-dev \
        gnuplot-x11 \
        libopenblas-base libatlas3-base \
        ghostscript pstoedit octave-info && \
    pip install -U \
         sympy && \
    pip3 install -U \
        octave_kernel && \
    python3 -m octave_kernel.install && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

USER $DOCKER_USER

RUN octave --no-gui --eval "pkg install -forge symbolic odepkg"

USER root
WORKDIR $DOCKER_HOME