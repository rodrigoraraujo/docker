FROM ubuntu:latest

MAINTAINER Rodrigo Ramalho Araujo <rodrigoraraujo@gmail.com | @maxrodrigho>

ARG CONTEXT_DIR=/context/
ARG JAVA_SDK=jdk-7u80-linux-x64.tar.gz
ARG JAVA_HOME=/opt/jdk1.7.0_80

ENV JAVA_SDK ${JAVA_SDK:-jdk-7u80-linux-x64.tar.gz}
ENV JAVA_HOME ${JAVA_HOME:-/opt/jdk1.7.0_80}

RUN apt-get clean all
RUN apt-get update
RUN apt-get install -y unzip
RUN apt-get install -y curl
RUN apt-get install -y vim

COPY ${CONTEXT_DIR}${JAVA_SDK} /opt/

RUN tar zxvf /opt/${JAVA_SDK} -C /opt; \
    rm /opt/${JAVA_SDK};
