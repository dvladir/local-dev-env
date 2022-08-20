FROM docker:dind

RUN mkdir -p /etc/docker/certs.d/docker.dvladir.work
COPY root.crt /etc/docker/certs.d/docker.dvladir.work/root.crt

RUN mkdir -p /etc/docker/certs.d/docker-push.dvladir.work
COPY root.crt /etc/docker/certs.d/docker-push.dvladir.work/root.crt