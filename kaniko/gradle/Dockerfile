FROM gcr.io/kaniko-project/executor:debug AS kaniko
FROM ubuntu:22.10

RUN apt-get update -y && \ 
    apt-get -y install git ssh bash curl && \
    apt-get install java-common && \
    curl -LO https://corretto.aws/downloads/latest/amazon-corretto-17-x64-linux-jdk.deb && \
    dpkg --install amazon-corretto-17-x64-linux-jdk.deb && \
    rm -f amazon-corretto-17-x64-linux-jdk.deb 

RUN wget -qO /usr/local/bin/yq https://github.com/mikefarah/yq/releases/latest/download/yq_linux_amd64 && \
    chmod a+x /usr/local/bin/yq

COPY --from=kaniko /kaniko/ /kaniko/

ENV PATH $PATH:/usr/local/bin:/kaniko
ENV DOCKER_CONFIG /kaniko/.docker/
ENV SSL_CERT_DIR /kaniko/ssl/certs