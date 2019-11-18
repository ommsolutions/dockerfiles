FROM adoptopenjdk/openjdk12:x86_64-alpine-jdk-12.0.2_10-slim

MAINTAINER David Werth <dw@omm-solutions.de>
LABEL vendor="OMM Solutions GmbH"
LABEL tools="node npm chromium alpine jdk openjdk adoptopenjdk java"

RUN apk add --no-cache \
    curl \
	openssh-client

# Installs latest Chromium package.
RUN echo @edge http://nl.alpinelinux.org/alpine/edge/community > /etc/apk/repositories \
    && echo @edge http://nl.alpinelinux.org/alpine/edge/main >> /etc/apk/repositories \
    && apk add --no-cache \
    libstdc++@edge \
    chromium@edge \
    harfbuzz@edge \
    nss@edge \
    freetype@edge \
    ttf-freefont@edge \
    && rm -rf /var/cache/* \
    && mkdir /var/cache/apk


ENV CHROME_BIN=/usr/bin/chromium-browser \
    CHROME_PATH=/usr/lib/chromium/

# Install Node
ARG version=latest

RUN curl -s 'https://nodejs.org/dist/'${version}'/'$( curl -s 'https://nodejs.org/dist/'${version}'/' | grep '"node-.*-linux-x64.tar.xz"' | awk -F'"' '{ print $2 }' ) | tar xvfJ - --strip-components=1 -C /usr/local && node --version
