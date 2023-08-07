FROM gcr.io/kaniko-project/executor:debug AS kaniko
# contains glibc to enable proprietary projects compiled against glibc 
# (e.g. OracleJDK, Anaconda) work on Alpine.
FROM frolvlad/alpine-glibc
RUN apk --update add sudo git openssh-client yq bash wget
COPY --from=kaniko /kaniko/ /kaniko/
RUN apk add --no-cache &&\
    wget -O /etc/apk/keys/amazoncorretto.rsa.pub https://apk.corretto.aws/amazoncorretto.rsa.pub && \
    echo "https://apk.corretto.aws" >> /etc/apk/repositories && \
    apk update &&\
    apk add amazon-corretto-17
ENV PATH $PATH:/usr/local/bin:/kaniko
ENV DOCKER_CONFIG /kaniko/.docker/
ENV DOCKER_CREDENTIAL_GCR_CONFIG /kaniko/.config/gcloud/docker_credential_gcr_config.json
ENV SSL_CERT_DIR /kaniko/ssl/certs