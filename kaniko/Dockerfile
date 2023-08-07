FROM gcr.io/kaniko-project/executor:debug AS kaniko
FROM amazoncorretto:17.0.8

RUN yum -y update && \ 
    yum -y install git ssh bash wget
RUN wget -qO /usr/local/bin/yq https://github.com/mikefarah/yq/releases/latest/download/yq_linux_amd64 && \
    chmod a+x /usr/local/bin/yq

COPY --from=kaniko /kaniko/ /kaniko/

ENV PATH $PATH:/usr/local/bin:/kaniko
ENV DOCKER_CONFIG /kaniko/.docker/
ENV SSL_CERT_DIR /kaniko/ssl/certs