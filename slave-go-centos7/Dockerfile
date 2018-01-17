FROM docker.io/fhwendy/jenkins-slave-base-centos7:latest

MAINTAINER Paul McCarthy <pamccart@redhat.com>

ENV PATH=$PATH:/usr/local/go/bin:/workspace/bin
ENV GOPATH=/workspace/

USER root

RUN yum -y install make wget && \
    curl -LO https://storage.googleapis.com/golang/go1.9.linux-amd64.tar.gz && \
    tar -C /usr/local -xzf go1.9.linux-amd64.tar.gz && \
    rm go1.9.linux-amd64.tar.gz && \
    wget https://github.com/Masterminds/glide/releases/download/v0.13.1/glide-v0.13.1-linux-amd64.tar.gz && \
    tar -C /tmp -xzf glide-v0.13.1-linux-amd64.tar.gz && \
    mv /tmp/linux-amd64/glide /usr/local/go/bin && \
    rm glide-v0.13.1-linux-amd64.tar.gz

USER 1001
