FROM jenkins/jenkins:lts

LABEL maintainer="Angel Aviel Domaoan <dev.tenshiamd@gmail.com>"

ARG PHP_VERSION=7.4
ENV PHP_VERSION $PHP_VERSION

ARG NODE_MAJOR_VERSION=14
ENV NODE_MAJOR_VERSION $NODE_MAJOR_VERSION

USER root

# Install dependencies
RUN apt-get update && apt-get install -y \
		apt-transport-https lsb-release ca-certificates \
		build-essential gnupg2 software-properties-common \
		libgtk2.0-0 libgtk-3-0 libnotify-dev libgconf-2-4 libnss3 \
		libxss1 libasound2 libxtst6 xauth xvfb \
       	libmcrypt-dev libreadline-dev \
       	libxml2-dev libxml++2.6-dev \
       	libpng-dev libssl-dev libcurl4-openssl-dev pkg-config

# Install PHP dependencies
RUN wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg
RUN echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list
RUN apt-get update && apt-get install -y php${PHP_VERSION} php${PHP_VERSION}-common \
		php${PHP_VERSION}-opcache php${PHP_VERSION}-cli \
		php${PHP_VERSION}-gd php${PHP_VERSION}-curl php${PHP_VERSION}-mysql php${PHP_VERSION}-exif \
		php${PHP_VERSION}-mbstring php${PHP_VERSION}-xml php${PHP_VERSION}-zip

## Installs NodeJS
RUN add-apt-repository -y -r ppa:chris-lea/node.js
RUN rm -f /etc/apt/sources.list.d/chris-lea-node_js-*.list
RUN rm -f /etc/apt/sources.list.d/chris-lea-node_js-*.list.save
RUN curl -sSL https://deb.nodesource.com/gpgkey/nodesource.gpg.key | apt-key add -
RUN echo "deb https://deb.nodesource.com/node_${NODE_MAJOR_VERSION}.x $(lsb_release -s -c) main" | tee /etc/apt/sources.list.d/nodesource.list
RUN echo "deb-src https://deb.nodesource.com/node_${NODE_MAJOR_VERSION}.x $(lsb_release -s -c) main" | tee -a /etc/apt/sources.list.d/nodesource.list
RUN apt-get update && apt-get install -y nodejs

## Installs Composer
RUN curl -sS https://getcomposer.org/installer | php
RUN chmod +x composer.phar
RUN mv composer.phar /usr/bin
RUN ln -s /usr/bin/composer.phar /usr/bin/composer

RUN apt-get clean
RUN apt-get autoremove -y --purge

USER jenkins
