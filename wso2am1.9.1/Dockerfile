FROM rodrigoraraujo/jdk:1.7_80

MAINTAINER Rodrigo Ramalho Araujo <rodrigoraraujo@gmail.com | @maxrodrigho>

ARG CONTEXT_DIR=/context/
ARG WSO2_PACK_NAME=wso2am-1.9.1.zip
ARG WSO2_PORT_OFFSET=0
ARG WSO2_FOLDER_NAME=wso2am
ARG WSO2_BUNDLE_NAME=wso2am-1.9.1

ENV WSO2_BUNDLE_NAME ${WSO2_BUNDLE_NAME:-wso2am-1.9.1}
ENV WSO2_FOLDER_NAME ${WSO2_FOLDER_NAME:-wso2am}
ENV WSO2_PORT_OFFSET ${WSO2_PORT_OFFSET:-0}

COPY ${CONTEXT_DIR}${WSO2_PACK_NAME} /opt/

RUN unzip -qq /opt/$WSO2_BUNDLE_NAME.zip -d /opt/; \
  mv /opt/${WSO2_BUNDLE_NAME} /opt/${WSO2_FOLDER_NAME}; \
  rm /opt/${WSO2_BUNDLE_NAME}.zip;  

WORKDIR /opt/${WSO2_FOLDER_NAME}/bin/

EXPOSE 9443 9763 8280 8243 7711 10397

CMD sh ./wso2server.sh -DportOffset=${WSO2_PORT_OFFSET}