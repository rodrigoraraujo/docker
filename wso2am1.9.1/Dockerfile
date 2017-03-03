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

ENV HTTPS_PORT 443
ENV HTTP_PORT 80
ENV HTTPS_MNGMNT_PORT 9443
ENV HTTP_MNGMNT_PORT 9763
ENV API_HTTPS_TRANS 8280
ENV API_HTTP_TRANS 8243
ENV API_THRIFT_TCP 7611
ENV API_THRIFT_SSL 7711
ENV API_THRIFT_CLIENT 10397

RUN export HTTPS_MNGMNT_PORT=$((HTTPS_MNGMNT_PORT+$WSO2_PORT_OFFSET))
RUN export HTTP_MNGMNT_PORT=$((HTTP_MNGMNT_PORT+$WSO2_PORT_OFFSET))
RUN export API_HTTPS_TRANS=$((API_HTTPS_TRANS+$WSO2_PORT_OFFSET))
RUN export API_HTTP_TRANS=$((API_HTTP_TRANS+$WSO2_PORT_OFFSET))
RUN export API_THRIFT_SSL=$((API_THRIFT_SSL+$WSO2_PORT_OFFSET))
RUN export API_THRIFT_TCP=$((API_THRIFT_TCP+$WSO2_PORT_OFFSET))
RUN export API_THRIFT_CLIENT=$((API_THRIFT_CLIENT+$WSO2_PORT_OFFSET))

EXPOSE $HTTPS_MNGMNT_PORT $HTTP_MNGMNT_PORT $API_HTTPS_TRANS $API_HTTP_TRANS $API_THRIFT_SSL $API_THRIFT_CLIENT $HTTPS_PORT $HTTP_PORT $API_THRIFT_TCP

CMD echo $(hostname -i) $WSO2_SERVER_NAME >> /etc/hosts; \
    sh ./wso2server.sh -DportOffset=${WSO2_PORT_OFFSET}