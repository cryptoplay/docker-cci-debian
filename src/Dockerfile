FROM debian:jessie

#ENV DOCKER_VERSION 17.03.1~ce-0~ubuntu-xenial
ENV COMPOSE_VERSION 1.13.0
ENV GOSS_VERSION 0.3.2
ENV BATS_VERSION 0.4.0

RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install --no-install-recommends -y \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg2 \
    software-properties-common && \
    curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add - && \
    add-apt-repository \
    "deb [arch=amd64] https://download.docker.com/linux/debian \
    $(lsb_release -cs) \
    stable" && \
    apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install --no-install-recommends -y \
    bash \
    docker-ce \
    file \
    git \
    gzip \
    make \
    python-dev \
    openssh-client \
    tar \
    && \
    apt-get autoremove -y && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
    curl "https://bootstrap.pypa.io/get-pip.py" -o "get-pip.py" && \
    python get-pip.py && \
    pip install --upgrade pip && \
    pip install docker-compose==${COMPOSE_VERSION} && \
    cd /tmp && \
    curl -sSL -o bats_v${BATS_VERSION}.tar.gz https://github.com/sstephenson/bats/archive/v${BATS_VERSION}.tar.gz && \
    tar -xf /tmp/bats_v${BATS_VERSION}.tar.gz && \
    bats-${BATS_VERSION}/install.sh /usr/local && \
    rm -fr /tmp/bats* && \
    curl -sSL -o /usr/bin/goss https://github.com/aelsabbahy/goss/releases/download/v${GOSS_VERSION}/goss-linux-amd64 && \
    chmod 0755 /usr/bin/goss && \
    :

COPY goss.yaml /
