FROM ubuntu:14.04
MAINTAINER Aaron Henshaw <aaronhenshaw@gmail.com>

ENV HOME /root

RUN apt-get update && \
    apt-get install -yq --no-install-recommends wget pwgen ca-certificates && \
    apt-get install -yq --no-install-recommends openjdk-7-jdk && \
    apt-get install -yq --no-install-recommends unzip curl git openssh-client build-essential software-properties-common && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

ENV JAVA_HOME /usr/lib/jvm/java-7-openjdk-amd64/
ENV GRAILS_VERSION 3.0.3

#########################
### INSTALL GRAILS w/ GVM
#########################
RUN curl -s get.gvmtool.net | bash
RUN ["/bin/bash", "-c", "source /root/.gvm/bin/gvm-init.sh"]
RUN ["/bin/bash", "-c", "-l", "gvm install grails"]

ENV GRAILS_HOME /root/.gvm/grails/current
ENV PATH $GRAILS_HOME/bin:$PATH

RUN grails -v;
