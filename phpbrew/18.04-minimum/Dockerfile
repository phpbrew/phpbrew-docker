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
 libcurl4 libcurl4-openssl-dev

SHELL ["/bin/bash", "-c"]
ARG PHP_VERSION=7.2
ARG PHP_DIST_NAME=$PHP_VERSION
ARG PHP_MIRROR=http://tw2.php.net
ARG DOWNLOADER=wget

ENV PHPBREW_ROOT /root/.phpbrew
ENV PHPBREW_HOME /root/.phpbrew
ENV PHPBREW_SET_PROMPT 1
RUN phpbrew init \
 && echo 'source $HOME/.phpbrew/bashrc' >> /root/.bashrc \
 && source ~/.phpbrew/bashrc \
 && phpbrew download --mirror $PHP_MIRROR --downloader $DOWNLOADER $PHP_VERSION

RUN source ~/.phpbrew/bashrc \
 && phpbrew --debug install --mirror $$PHP_MIRROR --downloader $DOWNLOADER --stdout \
              $PHP_VERSION as $PHP_DIST_NAME \
              +cli +phar +bz2 +xml +filter +mbregex +mbstring +posix +pcntl \
 && phpbrew use $PHP_DIST_NAME \
 && php -v

