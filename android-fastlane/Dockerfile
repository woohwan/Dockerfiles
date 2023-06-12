FROM alpine:3.18

LABEL saltware <whpark@saltware.co.kr>

ENV ANDROID_SDK_URL https://dl.google.com/android/repository/commandlinetools-linux-9477386_latest.zip
ENV ANDROID_API_LEVEL android-33
ENV ANDROID_BUILD_TOOLS_VERSION 33.0.2
ENV ANDROID_HOME /usr/local/android-sdk-linux
ENV ANDROID_VERSION 33
ENV PATH $PATH:$ANDROID_HOME/tools:$ANDROID_HOME/tools/bin:$ANDROID_HOME/platform-tools:$ANDROID_HOME/cmdline-tools/bin

# Install Amazon Correto JDK 17
RUN apk add --no-cache && \
    wget -O /etc/apk/keys/amazoncorretto.rsa.pub https://apk.corretto.aws/amazoncorretto.rsa.pub && \
    echo "https://apk.corretto.aws" >> /etc/apk/repositories && \
    apk update &&\
    apk add amazon-corretto-17 && \
    apk add curl && \
# create Android Dev Environemnt
    mkdir "$ANDROID_HOME" .android && \
    cd "$ANDROID_HOME" && \
    curl -o sdk.zip $ANDROID_SDK_URL && \
    unzip sdk.zip && \
    rm sdk.zip && \
# Download Android SDK
   yes | sdkmanager --licenses --sdk_root=$ANDROID_HOME && \
  sdkmanager --update --sdk_root=$ANDROID_HOME && \
  sdkmanager --sdk_root=$ANDROID_HOME "build-tools;${ANDROID_BUILD_TOOLS_VERSION}" \
      "platforms;android-${ANDROID_VERSION}" \
      "platform-tools" \
      "extras;android;m2repository" \
      "extras;google;m2repository"
# Install Fastlane
RUN apk add build-base git ruby && \
    gem install rake && \
    gem install fastlane -NV && \
    gem install bundler