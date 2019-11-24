FROM jenkins/jenkins:2.176.1-alpine

LABEL maintainer="Angel Aviel Domaoan <dev.tenshiamd@gmail.com>"

USER root

RUN apk update && apk add php7 php7-fpm php7-opcache php7-gd php7-mysqli \
php7-zlib php7-curl php7-json php7-phar php7-mcrypt php7-intl php7-imap \
php7-tidy php7-apcu php7-xdebug php7-mbstring php7-xml php7-pgsql php7-zip \
php7-simplexml php7-pdo php7-pdo_mysql php7-tokenizer php7-ctype php7-dom \
php7-iconv php7-xmlwriter php7-xmlreader php7-session php7-fileinfo php7-exif

## Installs node
RUN apk add nodejs-current nodejs-current-npm

## Installs composer
RUN curl -sS https://getcomposer.org/installer | php
RUN chmod +x composer.phar
RUN mv composer.phar /usr/bin
RUN ln -s /usr/bin/composer.phar /usr/bin/composer

USER jenkins

