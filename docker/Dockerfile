FROM ubuntu:18.04

LABEL maintainer="Iterative Inc"

RUN apt-get update && apt-get install -y --no-install-recommends --fix-missing \
    build-essential \
    apt-utils \
    apt-transport-https \
    ca-certificates \
    software-properties-common \
    pkg-config \
    curl \
    wget \
    unzip \
    gpg-agent && \
    add-apt-repository universe -y && \
    add-apt-repository ppa:git-core/ppa -y && \
    apt-get install -y git && \
    curl -sL https://deb.nodesource.com/setup_12.x | bash && \
    apt-get install -y nodejs  && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

# Install update pip and nodejs, install dvc and dvc-cml
ADD "./" "/dvc-cml"
RUN wget https://dvc.org/deb/dvc.list -O /etc/apt/sources.list.d/dvc.list && \
    apt update && apt install dvc && \
    npm install -g /dvc-cml && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

COPY ./docker/entrypoint.sh ./
CMD ["entrypoint.sh"]