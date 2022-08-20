FROM jenkins/jenkins:lts-jdk11
USER root
RUN apt-get update && apt-get install -y apt-transport-https \
    ca-certificates curl gnupg2 \
    software-properties-common
RUN curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add -
RUN apt-key fingerprint 0EBFCD88
RUN add-apt-repository \
    "deb [arch=amd64] https://download.docker.com/linux/debian \
    $(lsb_release -cs) stable"
RUN apt-get update && apt-get install -y docker-ce-cli

RUN rsync /custom_certs /usr/local/share/ca-certificates
RUN chmod -R 644 /usr/local/share/ca-certificates
RUN update-ca-certificates

USER jenkins
RUN jenkins-plugin-cli --plugins "blueocean:1.25.5 docker-workflow:1.28 locale:1.4 pipeline-npm:0.9.2"
