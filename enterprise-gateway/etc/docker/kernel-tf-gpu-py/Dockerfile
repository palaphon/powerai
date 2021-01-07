# Ubuntu:xenial
FROM ibmcom/tensorflow-ppc64le:1.15.3-gpu-jupyter

RUN apt-get update && apt-get install -yq \
    build-essential \
    libsm6 \
    libxext-dev \
    libxrender1 \
    netcat \
    python3-dev \
    unzip \
    && rm -rf /var/lib/apt/lists/*

RUN pip install future pycryptodomex\
    ipython_genutils

ADD ./kernel-launchers/bootstrap/bootstrap-kernel.sh /usr/local/bin
ADD ./kernel-launchers /usr/local/bin/kernel-launchers

USER root

RUN adduser --system --uid 1000 --gid 100 jovyan && \
    chown jovyan:users /usr/local/bin/bootstrap-kernel.sh && \
    chmod 0755 /usr/local/bin/bootstrap-kernel.sh && \
    chown -R jovyan:users /usr/local/bin/kernel-launchers


USER jovyan
ENV KERNEL_LANGUAGE python
CMD /usr/local/bin/bootstrap-kernel.sh
