FROM ubuntu:latest

MAINTAINER Rodrigo Ramalho Araujo <rodrigoraraujo@gmail.com | @maxrodrigho>

ENV WSO2_BUNDLE_NAME wso2am-1.10.0
ENV WSO2_FOLDER_NAME wso2am
ENV WSO2_PORT_OFFSET 0
ENV JAVA_SDK jdk-7u80-linux-x64

RUN apt-get update

RUN apt-get install -y unzip

RUN apt-get install -y curl

RUN apt-get install -y vim

EXPOSE 9443 9763 8280 8243 7711 10397

COPY ${JAVA_SDK}.tar.gz /opt/

COPY ${WSO2_BUNDLE_NAME}.zip /opt/

RUN unzip /opt/$WSO2_BUNDLE_NAME.zip -d /opt/ > /opt/${WSO2_FOLDER_NAME}.listfiles; \
  mv /opt/${WSO2_BUNDLE_NAME} /opt/${WSO2_FOLDER_NAME}; \
  rm /opt/${WSO2_BUNDLE_NAME}.zip; \
  rm /opt/${WSO2_FOLDER_NAME}.listfiles;

RUN tar zxvf /opt/${JAVA_SDK}.tar.gz -C /opt; \
    rm /opt/${JAVA_SDK}.tar.gz;

ENV JAVA_HOME /opt/jdk1.7.0_80

WORKDIR /opt/${WSO2_FOLDER_NAME}/bin/

CMD sh ./wso2server.sh -DportOffset=${WSO2_PORT_OFFSET}



