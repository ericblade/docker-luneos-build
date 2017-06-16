FROM ubuntu:latest
MAINTAINER Eric Blade (blade.eric@gmail.com)
RUN apt-get update
RUN apt-get install -y gawk wget git-core diffstat unzip texinfo build-essential chrpath libsdl1.2-dev xterm nodejs curl
RUN apt-get install -y cpio
RUN apt-get install -y bzr
RUN apt-get install -y vim-common # for xxd for node-js-modules
RUN curl -sL https://deb.nodesource.com/setup_4.x | bash -
RUN groupadd -r luneos && useradd --no-log-init -r -g luneos luneos
WORKDIR /home/luneos/luneos-build/webos-ports-env
RUN chown -R luneos:luneos /home/luneos
USER luneos
RUN mkdir -p /home/luneos/luneos-build/webos-ports-env/webos-ports/sstate-cache && mkdir -p /home/luneos/luneos-build/webos-ports-env/webos-ports/tmp-glibc
RUN ls -al /home/luneos/luneos-build/webos-ports-env/webos-ports/sstate-cache
RUN export ENV_NAME=testing && wget https://raw.github.com/webOS-ports/webos-ports-setup/$ENV_NAME/Makefile && make setup-webos-ports
ARG MACHINE="tenderloin"
ENV MACHINE=$MACHINE
WORKDIR /home/luneos/luneos-build/webos-ports-env/webos-ports
RUN cat ./setup-env >> /home/luneos/.bashrc

ENTRYPOINT ["/bin/bash"]
