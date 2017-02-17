FROM rodrigoraraujo/jdk:1.7_80

MAINTAINER Rodrigo Ramalho Araujo <rodrigoraraujo@gmail.com | @maxrodrigho>

ARG CONTEXT_DIR=/context/
ARG WSO2_PACK_NAME=wso2am-1.9.1.zip
ARG WSO2_PORT_OFFSET=0
ARG WSO2_FOLDER_NAME=wso2am
ARG WSO2_BUNDLE_NAME=wso2am-1.9.1
ARG WSO2_SERVER_NAME=wso2-local

ENV WSO2_BUNDLE_NAME ${WSO2_BUNDLE_NAME:-wso2am-1.9.1}
ENV WSO2_FOLDER_NAME ${WSO2_FOLDER_NAME:-wso2am}
ENV WSO2_PORT_OFFSET ${WSO2_PORT_OFFSET:-0}

COPY ${CONTEXT_DIR}${WSO2_PACK_NAME} /opt/

RUN unzip -qq /opt/$WSO2_BUNDLE_NAME.zip -d /opt/; \
  mv /opt/${WSO2_BUNDLE_NAME} /opt/${WSO2_FOLDER_NAME}; \
  rm /opt/${WSO2_BUNDLE_NAME}.zip;  

WORKDIR /opt/${WSO2_FOLDER_NAME}/bin/

ENV APIM_HOME /opt/${WSO2_FOLDER_NAME}
ENV WSO2_SERVER_NAME $WSO2_SERVER_NAME

RUN sed -i "s;<!--HostName>www.wso2.org</HostName-->;<HostName>$WSO2_SERVER_NAME</HostName>;g" ${APIM_HOME}/repository/conf/carbon.xml
RUN sed -i "s;<!--MgtHostName>mgt.wso2.org</MgtHostName-->;<MgtHostName>$WSO2_SERVER_NAME</MgtHostName>;g" ${APIM_HOME}/repository/conf/carbon.xml
RUN sed -i "s;<KeyValidatorClientType>ThriftClient</KeyValidatorClientType>;<KeyValidatorClientType>WSClient</KeyValidatorClientType>;g" ${APIM_HOME}/repository/conf/api-manager.xml
RUN sed -i "s;<!--ThriftServerHost>localhost</ThriftServerHost-->;<ThriftServerHost>$WSO2_SERVER_NAME</ThriftServerHost>;g" ${APIM_HOME}/repository/conf/api-manager.xml
RUN sed -i "s;\${carbon.local.ip};$WSO2_SERVER_NAME;g" ${APIM_HOME}/repository/conf/api-manager.xml
RUN sed -i "s;<!--<parameter name=\"HostnameVerifier\">DefaultAndLocalhost</parameter>-->;<parameter name=\"HostnameVerifier\">AllowAll</parameter>;g" ${APIM_HOME}/repository/conf/axis2/axis2.xml

EXPOSE 9443 9763 8280 8243 7711 10397

CMD echo $(hostname -i) $WSO2_SERVER_NAME >> /etc/hosts; \
    sh ./wso2server.sh -DportOffset=${WSO2_PORT_OFFSET}