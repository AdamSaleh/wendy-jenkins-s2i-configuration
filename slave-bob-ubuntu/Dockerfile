FROM docker.io/fhwendy/ubuntu-openjdk:precise

MAINTAINER Adam Saleh <asaleh@redhat.com>

ENV HOME=/home/jenkins

USER root
# Install Jenkins 

ENV MAVEN_VERSION=3.1.1

RUN apt-get update && \
    apt-get -y install make ant && \
    (curl -v https://www.apache.org/dist/maven/maven-3/$MAVEN_VERSION/binaries/apache-maven-$MAVEN_VERSION-bin.tar.gz | \
    tar -zx -C /usr/local) && \
    ln -sf /usr/local/apache-maven-$MAVEN_VERSION/bin/mvn /usr/local/bin/mvn && \
    mkdir -p $HOME/.m2
    mkdir -p /home/jenkins && \
    chown -R 1001:0 /home/jenkins && \
    chmod -R g+w /home/jenkins && \
    wget https://github.com/openshift/origin/releases/download/v1.3.0/openshift-origin-client-tools-v1.3.0-3ab7af3d097b57f933eccef684a714f2368804e7-linux-64bit.tar.gz && \
    tar -xvzf openshift-origin-client-tools-v1.3.0-3ab7af3d097b57f933eccef684a714f2368804e7-linux-64bit.tar.gz && \
    mv openshift*/oc /usr/local/bin && \
    rm -rf openshift-origin-client-tools-*


COPY contrib/bin/nvm_enable /usr/local/bin/nvm_enable

RUN echo default:x:1001:0:root:/home/jenkins:/bin/bash >> /etc/passwd

ADD contrib/bin/* /usr/local/bin/
# Install Ruby
RUN chown -R 1001:0 $HOME && \
    chmod -R g+rw $HOME

ENV BASH_ENV=/usr/local/bin/nvm_enable \
    ENV=/usr/local/bin/nvm_enable \
    PROMPT_COMMAND=". /usr/local/bin/nvm_enable"

COPY contrib/bin/nvm_enable /usr/local/bin/nvm_enable

USER 1001

RUN export NVM_DIR="$HOME/.nvm" && \
    curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.0/install.sh | METHOD=script bash && \
    [ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh" && \
    nvm install 4.4 && \
    nvm use 4.4 && npm i -g grunt



#RUN apt-get update && apt-get install libnss3


# Run the Jenkins JNLP client
ENTRYPOINT ["/usr/local/bin/run-jnlp-client"]
