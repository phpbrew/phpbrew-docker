FROM ubuntu:18.04

LABEL MAINTAINER "Yo-An Lin <yoanlin93@gmail.com>"

ENV DEBIAN_FRONTEND "noninteractive"

ENV TZ "Asia/Taipei"

RUN apt-get update

RUN apt-get install -y --no-install-recommends \
 # phpbrew used tools
 curl wget git \
 # build tools
 build-essential bison autoconf automake autotools-dev re2c \
 # pcre extension
 libpcre3-dev \
 # readline extension
 libreadline7 libreadline-dev \
 libedit-dev libedit2 \
 # xml related dependencies
 libxml2 libxml2-dev \
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
 mysql-server mysql-client libmysqlclient-dev libmysqld-dev \
 # postgresql extension \
 postgresql postgresql-client postgresql-contrib

# configure timezone
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN apt-get install -y ca-certificates php7.2 php7.2-cli

# Install phpbrew
RUN wget -q -O /usr/bin/phpbrew https://raw.githubusercontent.com/phpbrew/phpbrew/master/phpbrew \
 && chmod +x /usr/bin/phpbrew

ARG PHP_VERSION=7.2

ENV PHPBREW_ROOT /root/.phpbrew

ENV PHPBREW_HOME /root/.phpbrew

ENV PHPBREW_SET_PROMPT 1

SHELL ["/bin/bash", "-c"]

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


