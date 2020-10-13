ARG DOCKER_BASE_IMAGE
FROM $DOCKER_BASE_IMAGE
MAINTAINER talbdev <lab>

# Arguments.
ARG PYTHON_VERSION
ARG PYTHON_BASE_URL
ARG PYTHON_PIP_VERSION
ARG PYTHON_PIP_BASE_URL

# Environment Variables.
ENV PATH /usr/local/bin:$PATH

# Misc and Tools.
RUN yum install -y \
        gcc \
        make \
        openssl-devel \
        bzip2-devel \
        libffi-devel \
        sqlite-devel \
        python3-dev \
        ncurses-devel \
        zlib-devel \
        zlib1g-dev \
        wget \
        git \
        curl \
        nano \
    && yum -y groupinstall development \
    && yum clean all \
    && rm -rf /var/cache/yum

# Install Python.
RUN set -ex \
    && wget -q ${PYTHON_BASE_URL}/${PYTHON_VERSION}/Python-${PYTHON_VERSION}.tgz \
    && tar xzf Python-${PYTHON_VERSION}.tgz \
    && cd Python-${PYTHON_VERSION} \
    && ./configure \
        --enable-optimizations \
    && make altinstall \
    && cd .. && rm -rf Python-${PYTHON_VERSION}*

# Set sym links.
RUN cd /usr/local/bin \
    && ln -s idle3.8 idle \
    && ln -s pydoc3.8 pydoc \
    && ln -s python3.8 python \
    && ln -s python3.8 python3 \
    && ln -s python3.8m-config python-config \
    && ln -s pyvenv-3.8 pyvenv

# Install Pip.
RUN curl -fsSL -o /tmp/pip-linux-x64.tar.gz ${PYTHON_PIP_BASE_URL}/${PYTHON_PIP_VERSION}/pip-${PYTHON_PIP_VERSION}.tar.gz \
    && tar -xzf /tmp/pip-linux-x64.tar.gz -C /tmp/ \
    && cd /tmp/pip-${PYTHON_PIP_VERSION} && python setup.py install \
    && rm -rf /tmp/pip-linux-x64.tar.gz \
    && rm -rf pip-${PYTHON_PIP_VERSION}

CMD ["python3"]
