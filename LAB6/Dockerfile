FROM alpine:latest
# Environment variables
ENV TZ=Europe/Moscow \
    TOMCAT_MAJOR=10 \
    TOMCAT_VERSION=10.1.30 \
    CATALINA_HOME=/opt/tomcat
# install JAVA 
RUN apk -U upgrade --update && \
    apk add curl && \
    apk add ttf-dejavu \
    apk add tzdata gunzip bash


# install tomcat                                            
RUN curl -jkSL -o /tmp/apache-tomcat.tar.gz https://dlcdn.apache.org/tomcat/tomcat-${TOMCAT_MAJOR}/v${TOMCAT_VERSION}/bin/apache-tomcat-${TOMCAT_VERSION}.tar.gz && \
    gunzip /tmp/apache-tomcat.tar.gz && \
    tar -C /opt -xf /tmp/apache-tomcat.tar && \
    ln -s /opt/apache-tomcat-$TOMCAT_VERSION $CATALINA_HOME
#install git maven
RUN apk add git --no-cache &&\
    apk add maven &&\
    apk clean && \
    rm -rf /tmp/* /var/cache/apk/*
# cleanup




EXPOSE 8080

COPY startup.sh /opt/startup.sh

ENTRYPOINT /opt/startup.sh

WORKDIR $CATALINA_HOME

    RUN mkdir -p /app && \
    cd ./app && \
    git clone https://github.com/boxfuse/boxfuse-sample-java-war-hello.git &&  \
    cd ./boxfuse-sample-java-war-hello && \
    mvn -p 
COPY ./catalina.sh  /app
EXPOSE 8080

CMD [“catalina.sh”, “run”]