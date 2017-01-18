FROM openshift/jenkins-slave-base-centos7

MAINTAINER Michael Nairn <mnairn@redhat.com>

ENV BASH_ENV=/usr/local/bin/nvm_enable \
    ENV=/usr/local/bin/nvm_enable \
    PROMPT_COMMAND=". /usr/local/bin/nvm_enable"

COPY contrib/bin/nvm_enable /usr/local/bin/nvm_enable

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

RUN chown -R 1001:0 $HOME && \
    chmod -R g+rw $HOME

USER 1001
