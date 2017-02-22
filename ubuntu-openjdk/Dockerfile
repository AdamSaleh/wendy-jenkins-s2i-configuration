FROM ubuntu:12.04.5

MAINTAINER Adam Saleh <asaleh@redhat.com>

USER root
# Install headless Java

ENV MAVEN_VERSION=3.1.1

RUN apt-get update && \
    apt-get -y install software-properties-common python-software-properties && \
    add-apt-repository -y ppa:openjdk-r/ppa && \
    apt-get update && \
    apt-get -y install make ant bc curl wget gettext git openjdk-8-jdk lsof unzip zip && \
    (curl -v https://www.apache.org/dist/maven/maven-3/$MAVEN_VERSION/binaries/apache-maven-$MAVEN_VERSION-bin.tar.gz | \
    tar -zx -C /usr/local) && \
    ln -sf /usr/local/apache-maven-$MAVEN_VERSION/bin/mvn /usr/local/bin/mvn && \
    mkdir -p /var/log/feedhenry/core/ && \
    chown -R 1001:0 /var/log/feedhenry/core/ && \
    chmod -R g+w /var/log/feedhenry/core/ && \
    mkdir -p /home/jenkins/.m2 && \
    echo 127.0.0.1 loghost >> /etc/hosts && \
    wget http://ftp.us.debian.org/debian/pool/main/n/nss-wrapper/libnss-wrapper_1.1.3-1_amd64.deb && \
    dpkg -i libnss-wrapper_1.1.3-1_amd64.deb && \
    apt-get install -f 
