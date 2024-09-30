FROM alpine:latest
# Environment variables
ENV TZ=Europe/Moscow \
    TOMCAT_MAJOR=10 \
    TOMCAT_VERSION=10.1.30 \
    CATALINA_HOME=/opt/tomcat
# install JAVA 
RUN apk update && \
    apk add curl && \
    apk add ttf-dejavu && \
    apk add tzdata && \
    apk add unzip && \
    apk add bash && \
    apk add openjdk21


# install tomcat                                            
RUN curl -jkSL -o /tmp/apache-tomcat.tar.gz https://dlcdn.apache.org/tomcat/tomcat-${TOMCAT_MAJOR}/v${TOMCAT_VERSION}/bin/apache-tomcat-${TOMCAT_VERSION}.tar.gz && \
    gunzip /tmp/apache-tomcat.tar.gz && \
    tar -C /opt -xf /tmp/apache-tomcat.tar && \
    ln -s /opt/apache-tomcat-$TOMCAT_VERSION $CATALINA_HOME
#install git maven
RUN apk add git --no-cache && \
    apk add maven && \
    rm -rf /tmp/* /var/cache/apk/*

RUN mkdir -p ./app && \
    cd ./app && \
    git clone https://github.com/boxfuse/boxfuse-sample-java-war-hello.git &&  \
    cd ./boxfuse-sample-java-war-hello && \
    mvn package && \
    cp ./boxfuse-sample-java-war-hello/target/*.war $CATALINA_HOME/webapps/

WORKDIR $CATALINA_HOME

    
#COPY ./catalina.sh  /app
EXPOSE 8080

CMD [“catalina.sh”, “run”]