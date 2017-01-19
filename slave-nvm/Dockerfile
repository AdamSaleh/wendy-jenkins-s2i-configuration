FROM openshift/jenkins-slave-base-centos7

MAINTAINER Michael Nairn <mnairn@redhat.com>

# Install Ruby

RUN curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.0/install.sh | bash
RUN yum -y install make gcc-c++
RUN export NVM_DIR="$HOME/.nvm" && \
    [ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh" && \
    nvm install 0.10 && \
    nvm install 4.4 

RUN yum -y install memcached
COPY contrib/mongodb-org.repo /etc/yum.repos.d/mongodb-org.repo
RUN yum -y install mongodb-org
RUN yum -y install python-setuptools
RUN yum -y install wget bzip2
RUN wget https://github.com/stedolan/jq/releases/download/jq-1.5/jq-linux64 -O /usr/bin/jq
RUN chmod +x /usr/bin/jq
# RUN easy_install supervisor

# COPY config/supervisord.conf /etc/supervisord.conf

RUN mkdir -p /data/db
RUN chown -R 1001:0 /data/db
RUN mkdir -p /var/log/supervisor/

RUN chown -R 1001:0 $HOME && \
    chmod -R g+rw $HOME

COPY contrib/run-jnlp-client /usr/local/bin/run-jnlp-client
COPY config/npmrc /etc/npmrc 
COPY config/npmrc $HOME/.npmrc 
RUN chmod -R a+x /usr/local/bin/run-jnlp-client
RUN mkdir -p /opt/feedhenry/fh-dynoman/dynos/
RUN chmod -R 777 /opt/feedhenry/fh-dynoman/dynos/

RUN export NVM_DIR="$HOME/.nvm" && \
    [ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh" && \
    nvm use 0.10 && npm i -g grunt && \
    nvm use 4.4 && npm i -g grunt 
 
USER 1001

EXPOSE 27017
EXPOSE 28017

