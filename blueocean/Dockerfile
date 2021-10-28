FROM jenkins/jenkins:2.303.2-lts-jdk11
ARG ks_pass
EXPOSE 8083
ENV JENKINS_OPTS="--httpPort=-1 --httpsPort=8083 --httpsKeyStore=/usr/local/etc/certs/jenkins.jks --httpsKeyStorePassword=${ks_pass}"
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
USER jenkins
COPY jenkins.jks /usr/local/etc/certs/jenkins.jks
RUN jenkins-plugin-cli --plugins "blueocean:1.24.7 docker-workflow:1.26 locale:1.4 pipeline-npm:0.9.2"