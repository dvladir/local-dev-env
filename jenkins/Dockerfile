FROM jenkins/jenkins:2.289.2-lts-jdk11
ARG HOST_JENKINS_UID=1001
ARG HOST_JENKINS_GID=1001
ARG HOST_DOCKER_GID=967
USER root
RUN apt-get update && apt-get install -y apt-transport-https \
    ca-certificates curl gnupg2 \
    software-properties-common
RUN curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add -
RUN apt-key fingerprint 0EBFCD88
RUN add-apt-repository \
    "deb [arch=amd64] https://download.docker.com/linux/debian \
    $(lsb_release -cs) stable"
RUN apt-get update && apt-get install -y docker-ce docker-ce-cli containerd.io
RUN curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" \
     -o /usr/local/bin/docker-compose && \
 chmod +x /usr/local/bin/docker-compose && \
 ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
RUN groupmod -g $HOST_DOCKER_GID docker
RUN groupmod -g $HOST_JENKINS_GID jenkins
RUN usermod -u $HOST_JENKINS_GID jenkins
RUN usermod -aG docker jenkins
USER jenkins