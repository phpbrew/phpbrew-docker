ARG PHPBREW_BASE_IMAGE
FROM ${PHPBREW_BASE_IMAGE}

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
