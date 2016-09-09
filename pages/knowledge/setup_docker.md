---
title: Setup Docker
keywords: docker
sidebar: knowledge_sidebar
permalink: setup_docker.html
folder: knowledge
---

## Mac

## Ubuntu

### Prerequisites

* [Ubuntu](setup_ubuntu.html)

### Install needed packages

```shell
sudo apt-get install -y apt-transport-https ca-certificates
sudo apt-get install -y linux-image-extra-$(uname -r)
```

### Add the docker repository

```shell
sudo apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D
```

Create a file `/etc/apt/sources.list.d/docker.list` and put the repository url in it.

```shell
echo "deb https://apt.dockerproject.org/repo ubuntu-xenial main" | sudo tee /etc/apt/sources.list.d/docker.list
```

Now update the package database.

```shell
sudo apt-get update
```

### Install docker

```shell
sudo apt-get install -y docker-engine
```

### Add yourself to the docker group

This is in order to avoid prefixing `docker` with `sudo` everytime.

```shell
sudo usermod -aG docker $(whoami)
```

You probably need to logout/login for this to take effect.

### Install `docker-compose`

```shell
COMPOSE_VERSION=`git ls-remote https://github.com/docker/compose | grep refs/tags | grep -oP "[0-9]+\.[0-9]+\.[0-9]+$" | tail -n 1`
```

```shell
sudo sh -c "curl -L https://github.com/docker/compose/releases/download/${COMPOSE_VERSION}/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose"
```

```shell
sudo chmod +x /usr/local/bin/docker-compose
```

```shell
sudo sh -c "curl -L https://raw.githubusercontent.com/docker/compose/${COMPOSE_VERSION}/contrib/completion/bash/docker-compose > /etc/bash_completion.d/docker-compose"
```


## Links
* [https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-16-04](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-16-04)
* [https://docs.docker.com/engine/installation/linux/ubuntulinux](https://docs.docker.com/engine/installation/linux/ubuntulinux)
* [https://docs.docker.com/compose/install](https://docs.docker.com/compose/install)
* [https://gist.github.com/wdullaer/f1af16bd7e970389bad3](https://gist.github.com/wdullaer/f1af16bd7e970389bad3)

{% include links.html %}
