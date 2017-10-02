FROM jenkins
MAINTAINER CanteIbanez <flordecante.t.ibanez@gmail.com>

# Suppress apt installation warnings
ENV DEBIAN_FRONTEND=noninteractive


USER root

ARG DOCKER_GID=497

RUN groupadd -g ${DOCKER_GID:-497} docker


ARG DOCKER_ENGINE=1.10.2
ARG DOCKER_COMPOSE=1.6.2

RUN apt-get update -y && \
    apt-get install apt-transport-https curl python-dev python-setuptools gcc make -y && \
    easy_install pip

# Install Docker Engine
RUN apt-key adv --keyserver hkp://pgp.mit.edu:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D
RUN echo "deb https://apt.dockerproject.org/repo ubuntu-zesty main" > /etc/apt/sources.list.d/docker.list
RUN apt-get update -y
RUN apt-get purge lxc-docker* -y 
RUN apt-get install docker-engine -qqy
RUN usermod -aG docker jenkins
RUN usermod -aG users jenkins

# Install Docker Compose
RUN pip install docker-compose==${DOCKER_COMPOSE:-1.6.2} && \
    pip install ansible boto boto3

# Change to jenkins user
USER jenkins

# Add Jenkins plugins
COPY plugins.txt /usr/share/jenkins/plugins.txt
RUN /usr/local/bin/plugins.sh /usr/share/jenkins/plugins.txt



























