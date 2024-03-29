FROM ubuntu:latest
 
MAINTAINER Olaf Horstmann <oh@omm-solutions.de>
LABEL vendor="OMM Solutions GmbH"
LABEL tools="libgtk chrome node npm yarn python pip electron xvfb"

RUN dpkg --add-architecture i386

#RUN apt-get update
#RUN apt-get install -y gnupg2 software-properties-common
#ADD https://dl.winehq.org/wine-builds/Release.key /wine.key
#RUN apt-key add /wine.key
#RUN apt-add-repository https://dl.winehq.org/wine-builds/ubuntu/
#Edit to update Docker Image

# Install deps
ENV TZ=Europe/Berlin
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update
RUN apt-get install -y \
    apt-transport-https \
    ca-certificates \
    curl \
    libgtk2.0-0 \
    gnupg \
    git \
    zip \
    unzip \
    groff-base \
    xvfb \
    default-jre \
#    winehq-stable \
    libgconf-2-4 \
    libgbm-dev \
    udev \
    libx11-dev \
    libxtst-dev \
    libpng++-dev \
    libxss1 \
    --no-install-recommends

# Get Chrome sources
RUN curl -sSL https://dl.google.com/linux/linux_signing_key.pub | apt-key add - \
    && echo "deb [arch=amd64] https://dl.google.com/linux/chrome/deb/ stable main" > /etc/apt/sources.list.d/google-chrome.list

# Install latest stable chrome
RUN apt-get update && apt-get install -y \
    google-chrome-stable \
    --no-install-recommends

# Get yarn sources
RUN curl -sSL https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - \
    && echo "deb [arch=amd64] https://dl.yarnpkg.com/debian/ stable main" > /etc/apt/sources.list.d/yarn.list

# Install yarn pinned version
RUN apt-get update && apt-get install -y \
    yarn=1.3.2-1 \
    --no-install-recommends

# Uncomment to install Python
RUN apt-get update && apt-get install -y \
    python2.7

# Nodejs
RUN curl -sL https://deb.nodesource.com/setup_14.x | bash -
RUN apt-get install -y nodejs
RUN apt-get install -y gcc g++ make

RUN npm install -g npm@7.15.0

RUN npm install electron -g --unsafe-perm=true

# Uncomment to install MongoDB
# RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 0C49F3730359A14518585931BC711F9BA15703C6
# RUN echo "deb [ arch=amd64,arm64 ] http://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/3.4 multiverse" | tee /etc/apt/sources.list.d/mongodb-org-3.4.list
# RUN apt-get update && apt-get install -y mongodb-org-server

# Install aws cli
# RUN pip install --upgrade pip setuptools
# RUN pip install --upgrade awscli

# Install OWASP ZAP (Zed Attack Proxy)
RUN mkdir /opt/zap/ \
    && curl -sSL https://github.com/zaproxy/zaproxy/releases/download/v2.8.0/ZAP_2.8.0_Linux.tar.gz > zap.tar.gz \
    && tar -xzvf zap.tar.gz -C /opt/zap/ \
    && rm zap.tar.gz
