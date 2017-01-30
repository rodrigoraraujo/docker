FROM ubuntu:latest

MAINTAINER Rodrigo Ramalho Araujo <rodrigoraraujo@gmail.com | @maxrodrigho>

ARG COMMOM_DIR=/commom/
ARG WSO2_PACK_NAME=wso2am-1.10.0.zip
ARG JAVA_SDK=jdk-7u80-linux-x64.tar.gz

ENV WSO2_BUNDLE_NAME wso2am-1.10.0
ENV WSO2_FOLDER_NAME wso2am
ENV WSO2_PORT_OFFSET 0
ENV JAVA_HOME /opt/jdk1.7.0_80

COPY ${COMMOM_DIR}${JAVA_SDK} /opt/
COPY ${COMMOM_DIR}${WSO2_PACK_NAME} /opt/

RUN apt-get clean
RUN apt-get update
RUN apt-get install -y unzip
RUN apt-get install -y curl
RUN apt-get install -y vim
RUN unzip /opt/$WSO2_BUNDLE_NAME.zip -d /opt/ > /opt/${WSO2_FOLDER_NAME}.listfiles; \
  mv /opt/${WSO2_BUNDLE_NAME} /opt/${WSO2_FOLDER_NAME}; \
  rm /opt/${WSO2_BUNDLE_NAME}.zip; \
  rm /opt/${WSO2_FOLDER_NAME}.listfiles;
RUN tar zxvf /opt/${JAVA_SDK} -C /opt; \
    rm /opt/${JAVA_SDK};

WORKDIR /opt/${WSO2_FOLDER_NAME}/bin/

EXPOSE 9443 9763 8280 8243 7711 10397

CMD sh ./wso2server.sh -DportOffset=${WSO2_PORT_OFFSET}



