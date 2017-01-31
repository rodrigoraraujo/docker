FROM rodrigoraraujo/jdk:1.7_80

MAINTAINER Rodrigo Ramalho Araujo <rodrigoraraujo@gmail.com | @maxrodrigho>

ARG CONTEXT_DIR=/context/
ARG WSO2_PACK_NAME=wso2bam-2.5.0.zip
ARG WSO2_PORT_OFFSET=3
ARG WSO2_FOLDER_NAME=wso2bam
ARG WSO2_BUNDLE_NAME=wso2bam-2.5.0

ENV WSO2_BUNDLE_NAME ${WSO2_BUNDLE_NAME:-wso2bam-2.5.0}
ENV WSO2_FOLDER_NAME ${WSO2_FOLDER_NAME:-wso2bam}
ENV WSO2_PORT_OFFSET ${WSO2_PORT_OFFSET:-0}

COPY ${CONTEXT_DIR}${WSO2_PACK_NAME} /opt/

RUN unzip -qq /opt/$WSO2_BUNDLE_NAME.zip -d /opt/; \
  mv /opt/${WSO2_BUNDLE_NAME} /opt/${WSO2_FOLDER_NAME}; \
  rm /opt/${WSO2_BUNDLE_NAME}.zip;  

WORKDIR /opt/${WSO2_FOLDER_NAME}/bin/

EXPOSE 9446 9766 8283 8246 7714 10402 7614

CMD sh ./wso2server.sh -DportOffset=${WSO2_PORT_OFFSET}



