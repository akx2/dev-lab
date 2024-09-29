FROM alpine:latest
ENV TZ=Europe/Moscow
RUN apk update && \
    apk upgrade --available && sync \
    apk add --no-cache openjdk17 && \
    apk add git --no-cache &&\
    apk addmaven &&\
    apk add tomcat &&\
    apk clean
RUN mkdir -p /app && \
    cd ./app && \
    git clone https://github.com/boxfuse/boxfuse-sample-java-war-hello.git &&  \
    cd ./boxfuse-sample-java-war-hello\

