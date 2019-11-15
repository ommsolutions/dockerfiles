FROM adoptopenjdk/openjdk12:x86_64-alpine-jdk-12.0.2_10-slim

MAINTAINER David Werth <dw@omm-solutions.de>
LABEL vendor="OMM Solutions GmbH"
LABEL tools="node npm chrome alpine jdk openjdk adoptopenjdk java"

RUN apk add --no-cache \
    curl \
	openssh-client

# Get Chrome sources
RUN curl -sSL https://dl.google.com/linux/linux_signing_key.pub | apt-key add - \
    && echo "deb [arch=amd64] https://dl.google.com/linux/chrome/deb/ stable main" > /etc/apt/sources.list.d/google-chrome.list

# Install latest stable chrome
RUN apt-get update && apt-get install -y \
    google-chrome-stable \
    --no-install-recommends

# Install Node
ARG version=latest

RUN curl -s 'https://nodejs.org/dist/'${version}'/'$( curl -s 'https://nodejs.org/dist/'${version}'/' | grep '"node-.*-linux-x64.tar.xz"' | awk -F'"' '{ print $2 }' ) | tar xvfJ - --strip-components=1 -C /usr/local && node --version
