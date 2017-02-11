FROM oraclelinux:latest

MAINTAINER Rodrigo Ramalho Araujo | rodrigoraraujo@gmail.com

# Passwords can be supplied for the following two schemas in the
# starter database: SYS and SYSTEM
ARG ORACLE_PASSWORD=Welcome1

# HTTP port that will be used to access APEX admin page 
ARG ORACLE_HTTP_PORT=8080

# TNS port that will be used to configure listener 
ARG ORACLE_LISTENER_PORT=1521

# To start/stop listener and database instance up on system boot
ARG ORACLE_DBENABLE=y

# Oracle Database XE install pack location.
ARG ORACLE_XE_PACK=/context/oracle-xe-11.2.0-1.0.x86_64.rpm.zip

# Oracle package installation folder
ARG ORACLE_INST=/home/downloads/

COPY ${ORACLE_XE_PACK} /home/downloads/

RUN yum update -y -q
RUN yum install -y deltarpm
RUN yum install -y vim
RUN yum install -y curl
RUN yum install -y libaio
RUN yum install -y unzip
RUN yum install -y bc
RUN yum provides -y */netstat

RUN unzip -qq ${ORACLE_INST}oracle-xe-11.2.0-1.0.x86_64.rpm.zip -d ${ORACLE_INST}

RUN rpm -ivh ${ORACLE_INST}Disk1/oracle-xe-11.2.0-1.0.x86_64.rpm

RUN sed -i "s/ORACLE_PASSWORD=<value required>/ORACLE_PASSWORD=${ORACLE_PASSWORD}/g" ${ORACLE_INST}Disk1/response/xe.rsp    
RUN sed -i "s/ORACLE_CONFIRM_PASSWORD=<value required>/ORACLE_CONFIRM_PASSWORD=${ORACLE_PASSWORD}/g"  ${ORACLE_INST}Disk1/response/xe.rsp    
RUN sed -i "s/ORACLE_HTTP_PORT=<value required>/ORACLE_HTTP_PORT=${ORACLE_HTTP_PORT}/g" ${ORACLE_INST}Disk1/response/xe.rsp    
RUN sed -i "s/ORACLE_LISTENER_PORT=<value required>/ORACLE_LISTENER_PORT=${ORACLE_LISTENER_PORT}/g" ${ORACLE_INST}Disk1/response/xe.rsp    
RUN sed -i "s/ORACLE_DBENABLE=<value required>/ORACLE_DBENABLE=${ORACLE_DBENABLE}/g" ${ORACLE_INST}Disk1/response/xe.rsp
    
RUN cat ${ORACLE_INST}Disk1/response/xe.rsp

ENV ORACLE_HOME /u01/app/oracle/product/11.2.0/xe
ENV ORACLE_SID XE
ENV PATH ${PATH}:${ORACLE_HOME}:${ORACLE_HOME}/bin

# !!! Don't forget to set --shm-size=<at least 2g> on creating either container command run or build. Otherwise the command bellow doesn't work !!!
RUN /etc/init.d/oracle-xe configure responseFile=${ORACLE_INST}Disk1/response/xe.rsp

RUN rm -rf ${ORACLE_INST}

CMD /etc/init.d/oracle-xe start

