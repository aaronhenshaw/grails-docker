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
ENV TOMCAT_MAJOR_VERSION 7
ENV TOMCAT_MINOR_VERSION 7.0.55
ENV CATALINA_HOME /tomcat
ENV GRAILS_VERSION 3.0.3

ADD create_tomcat_admin_user.sh /create_tomcat_admin_user.sh
ADD run.sh /run.sh
RUN chmod +x /*.sh

#########################
### INSTALL GRAILS w/ GVM
#########################
RUN curl -s get.gvmtool.net | bash
RUN ["/bin/bash", "-c", "source /root/.gvm/bin/gvm-init.sh"]
RUN ["/bin/bash", "-c", "-l", "gvm install grails"]

ENV GRAILS_HOME /root/.gvm/grails/current
ENV PATH $GRAILS_HOME/bin:$PATH

RUN grails -v;

##################
### INSTALL TOMCAT
##################
RUN wget -q https://archive.apache.org/dist/tomcat/tomcat-${TOMCAT_MAJOR_VERSION}/v${TOMCAT_MINOR_VERSION}/bin/apache-tomcat-${TOMCAT_MINOR_VERSION}.tar.gz && \
    wget -qO- https://archive.apache.org/dist/tomcat/tomcat-${TOMCAT_MAJOR_VERSION}/v${TOMCAT_MINOR_VERSION}/bin/apache-tomcat-${TOMCAT_MINOR_VERSION}.tar.gz.md5 | md5sum -c - && \
    tar zxf apache-tomcat-*.tar.gz && \
    rm apache-tomcat-*.tar.gz && \
    mv apache-tomcat* tomcat
