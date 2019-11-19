FROM adoptopenjdk/openjdk12:x86_64-alpine-jdk-12.0.2_10-slim

MAINTAINER David Werth <dw@omm-solutions.de>
LABEL vendor="OMM Solutions GmbH"
LABEL tools="node npm chromium alpine jdk openjdk adoptopenjdk java"

RUN apk add --no-cache \
    curl \
	openssh-client \
	bash

# Installs latest Chromium package.
RUN apk add --no-cache \
    libstdc++ \
    gifsicle \
    pngquant \
    optipng \
    libjpeg-turbo-utils \
    udev \
    mesa-gles \
    mesa-egl \
    harfbuzz \
    nss \
    freetype \
    ttf-freefont \
    ttf-opensans \
    chromium \
    chromium-chromedriver

ENV CHROME_BIN=/usr/bin/chromium-browser \
    CHROME_PATH=/usr/lib/chromium/ \
    LIGHTHOUSE_CHROMIUM_PATH=/usr/bin/chromium-browser

RUN mkdir /usr/lib/chromium/swiftshader
RUN ln -s /usr/lib/libGLESv2.so.2  /usr/lib/chromium/swiftshader/libGLESv2.so
RUN ln -s /usr/lib/libEGL.so.1  /usr/lib/chromium/swiftshader/libEGL.so

# Install Node
ARG version=latest-erbium
RUN curl -s 'https://nodejs.org/dist/'${version}'/'$( curl -s 'https://nodejs.org/dist/'${version}'/' | grep '"node-.*-linux-x64.tar.xz"' | awk -F'"' '{ print $2 }' ) | tar xvfJ - --strip-components=1 -C /usr/local && node --version
