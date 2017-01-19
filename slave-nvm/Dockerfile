FROM openshift/jenkins-slave-base-centos7

MAINTAINER Michael Nairn <mnairn@redhat.com>

# Install Ruby

RUN curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.0/install.sh | bash
RUN yum -y install make gcc-c++
RUN export NVM_DIR="$HOME/.nvm" && \
    [ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh" && \
    nvm install 0.10 && \
    nvm install 4.4 

RUN export NVM_DIR="$HOME/.nvm" && \
    [ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh" && \
    nvm use 0.10 && npm i -g grunt && npm i -g jq && npm i -g commander  && npm i -g async  && npm i -g rimraf  && npm i -g winston  && npm i -g colors 

RUN export NVM_DIR="$HOME/.nvm" && \
    [ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh" && \
    nvm use 4.4 && npm i -g grunt && npm i -g jq && npm i -g commander  && npm i -g async  && npm i -g rimraf  && npm i -g winston  && npm i -g colors

RUN yum -y install memcached
COPY contrib/mongodb-org.repo /etc/yum.repos.d/mongodb-org.repo
RUN yum -y install mongodb-org
RUN yum -y install python-setuptools
RUN easy_install supervisor

COPY config/supervisord.conf /etc/supervisord.conf

RUN mkdir -p /data/db
RUN chown -R 1001:0 /data/db
RUN mkdir -p /var/log/supervisor/

RUN chown -R 1001:0 $HOME && \
    chmod -R g+rw $HOME

USER 1001

EXPOSE 27017
EXPOSE 28017

COPY /contrib/run-jnlp-client /usr/local/bin/run-jnlp-client
