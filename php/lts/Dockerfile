FROM jenkins/jenkins:lts

LABEL maintainer="Angel Aviel Domaoan <dev.tenshiamd@gmail.com>"

USER root

ARG PHP_VERSION=7.3
ENV PHP_VERSION $PHP_VERSION

# Install Pdependencies
RUN apt-get update && apt-get install -y \
       libmcrypt-dev libreadline-dev \
       libxml2-dev libxml++2.6-dev \
       libpng-dev libssl-dev libcurl4-openssl-dev pkg-config

RUN apt-get update && apt-get install -y apt-transport-https lsb-release ca-certificates
RUN wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg
RUN echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list

# Install dependencies
RUN apt-get update && apt-get install -y php${PHP_VERSION} php${PHP_VERSION}-common php${PHP_VERSION}-opcache php${PHP_VERSION}-cli \
		php${PHP_VERSION}-gd php${PHP_VERSION}-curl php${PHP_VERSION}-mysql php${PHP_VERSION}-exif php${PHP_VERSION}-mbstring php${PHP_VERSION}-xml php${PHP_VERSION}-zip

## Installs NodeJS
RUN curl -sL https://deb.nodesource.com/setup_11.x | bash -
RUN apt-get update -qq && apt-get install -y build-essential nodejs

## Installs Composer
RUN curl -sS https://getcomposer.org/installer | php
RUN chmod +x composer.phar
RUN mv composer.phar /usr/bin
RUN ln -s /usr/bin/composer.phar /usr/bin/composer

RUN apt-get update && apt-get install -y libgtk2.0-0 libgtk-3-0 libnotify-dev libgconf-2-4 libnss3 libxss1 libasound2 libxtst6 xauth xvfb

USER jenkins
