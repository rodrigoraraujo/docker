FROM oraclelinux:latest

MAINTAINER Rodrigo Ramalho Araujo | rodrigoraraujo@gmail.com

ARG CONTEXT_DIR=/context/
ARG JAVA_SDK=jdk-7u80-linux-x64.tar.gz
ARG JAVA_HOME=/opt/jdk1.7.0_80/

ENV JAVA_SDK ${JAVA_SDK:-jdk-7u80-linux-x64.tar.gz}
ENV JAVA_HOME ${JAVA_HOME:-/opt/jdk1.7.0_80}
ENV PATH ${PATH}:${JAVA_HOME}:${JAVA_HOME}/bin

RUN yum update -y -q
RUN yum install -y deltarpm
RUN yum install -y vim
RUN yum install -y tar
RUN yum install -y curl
RUN yum install -y libaio
RUN yum install -y unzip
RUN yum install -y bc
RUN yum install -y deltarpm

COPY ${CONTEXT_DIR}${JAVA_SDK} /opt/
COPY ${CONTEXT_DIR}ofm_osb_generic_11.1.1.7.0_disk1_1of1.zip /home/
COPY ${CONTEXT_DIR}ofm_soa_generic_11.1.1.7.0_disk1_1of2.zip /home/
COPY ${CONTEXT_DIR}ofm_soa_generic_11.1.1.7.0_disk1_2of2.zip /home/

RUN tar zxvf /opt/${JAVA_SDK} -C /opt; \
    rm /opt/${JAVA_SDK};

CMD /bin/bash