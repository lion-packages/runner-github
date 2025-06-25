FROM ubuntu:22.04

ARG DEBIAN_FRONTEND=noninteractive

RUN useradd -m lion && echo 'lion:lion' | chpasswd && usermod -aG sudo lion && usermod -s /bin/bash lion

RUN apt-get update && apt-get install -y \
    curl \
    gnupg \
    ca-certificates \
    lsb-release \
    software-properties-common \
    apt-transport-https \
    sudo

RUN for pkg in docker.io docker-doc docker-compose docker-compose-v2 podman-docker containerd runc; do \
      apt-get remove -y $pkg || true; \
    done

RUN apt-get update && \
    apt-get install -y ca-certificates curl gnupg

RUN install -m 0755 -d /etc/apt/keyrings && \
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc && \
    chmod a+r /etc/apt/keyrings/docker.asc

RUN echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] \
    https://download.docker.com/linux/ubuntu $(. /etc/os-release && echo ${UBUNTU_CODENAME:-$VERSION_CODENAME}) stable" \
    > /etc/apt/sources.list.d/docker.list

RUN apt-get update && \
    apt-get install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

RUN usermod -aG docker lion

WORKDIR /var/www/html

COPY . .
