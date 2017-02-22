FROM ubuntu:12.04.5

MAINTAINER Adam Saleh <asaleh@redhat.com>

USER root
# Install headless Java

RUN apt-get update && \
    apt-get -y install software-properties-common python-software-properties && \
    add-apt-repository -y ppa:openjdk-r/ppa && \
    apt-get update && \
    apt-get -y install make bc curl wget gettext git openjdk-8-jdk lsof unzip zip && \
    wget http://ftp.us.debian.org/debian/pool/main/n/nss-wrapper/libnss-wrapper_1.1.3-1_amd64.deb && \
    dpkg -i libnss-wrapper_1.1.3-1_amd64.deb && \
    apt-get install -f 
