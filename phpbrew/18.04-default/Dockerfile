FROM ubuntu:18.04

LABEL MAINTAINER "Yo-An Lin <yoanlin93@gmail.com>"

ENV DEBIAN_FRONTEND "noninteractive"

ENV TZ "Asia/Taipei"

RUN apt-get update

RUN apt-get install -y --no-install-recommends \
 # phpbrew used tools
 curl wget git ca-certificates \
 # phpbrew runtime
 php7.2-cli php7.2-phar php7.2-json php7.2-readline php7.2-bz2 \
 # timezone data
 tzdata

# configure timezone
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# install phpbrew binary
RUN wget -q -O /usr/bin/phpbrew https://raw.githubusercontent.com/phpbrew/phpbrew/master/phpbrew \
 && chmod +x /usr/bin/phpbrew

# install base build dependencies for php
RUN apt-get install  -y --no-install-recommends \
 build-essential bison autoconf automake autotools-dev re2c


# install extension build dependencies for php
RUN apt-get install -y --no-install-recommends \
 # pcre extension
 libpcre3-dev \
 # for compression
 libbz2-dev \
 # zip extension
 libzip4 libzip-dev \
 # readline extension
 libreadline7 libreadline-dev \
 libedit-dev libedit2 \
 # xml related dependencies
 libxml2 libxml2-dev \
 libxslt1-dev libxslt1.1 \
 # openssl dependencies
 libssl-dev openssl \
 # curl extension dependencies
 libcurl4 libcurl4-openssl-dev \
 # intl extension dependencies
 gettext \
 libicu-dev \
 # encryption extension related dependencies
 libmcrypt-dev libmcrypt4 \
 libmhash-dev libmhash2 \
 # gd extension related dependencies
 libgd-dev libgd3 \
 libfreetype6 libfreetype6-dev \
 libpng-dev libpng16-16 \
 libjpeg-dev libjpeg8-dev libjpeg8 \
 libxpm4 libltdl7 libltdl-dev \
 # mysql extension \
 mysql-client libmysqlclient-dev libmysqld-dev \
 # postgresql extension \
 postgresql postgresql-client postgresql-contrib

SHELL ["/bin/bash", "-c"]
ARG PHP_VERSION=7.2
ENV PHPBREW_ROOT /root/.phpbrew
ENV PHPBREW_HOME /root/.phpbrew
ENV PHPBREW_SET_PROMPT 1
RUN phpbrew init \
  && echo 'source $HOME/.phpbrew/bashrc' >> /root/.bashrc \
  && source ~/.phpbrew/bashrc \
  && phpbrew --debug install $PHP_VERSION as $PHP_VERSION \
              +default +bcmath +bz2 +calendar +cli +ctype +dom +fileinfo +filter +json \
              +mbregex +mbstring +mhash +pcntl +pcre  +phar +posix +readline +sockets \
              +tokenizer +xml +curl +zip +openssl=yes +fpm \
              # databases
              +pdo +sqlite +mysql \
              # i18n extensions
              +icu +intl +gettext \
              # performance
              +opcache
