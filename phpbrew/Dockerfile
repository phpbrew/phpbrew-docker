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

# phpbrew root stores the php installation
ENV PHPBREW_ROOT /root/.phpbrew

# phpbrew home stores the user preference
ENV PHPBREW_HOME /root/.phpbrew

ENV PHPBREW_BIN=/root/.phpbrew/bin

# enable bash prompt
ENV PHPBREW_SET_PROMPT 1

# init and setup phpbrew
RUN phpbrew init \
 && echo 'source $HOME/.phpbrew/bashrc' >> /root/.bashrc


ARG PHP_VERSION=7.2
ARG PHP_DIST_NAME=$PHP_VERSION
ARG PHP_MIRROR=http://us1.php.net
ARG DOWNLOADER=wget
ARG PHP_VARIANTS=

# predownload the distribution file
RUN source ~/.phpbrew/bashrc \
 && phpbrew download --mirror $PHP_MIRROR --downloader $DOWNLOADER $PHP_VERSION

# extract and install php
RUN source ~/.phpbrew/bashrc \
 && phpbrew --debug install --mirror $$PHP_MIRROR --downloader $DOWNLOADER --stdout \
              $PHP_VERSION as $PHP_DIST_NAME \
              +cli +phar +curl +json +bz2 +xml +filter +hash +mbregex +mbstring +posix +pcntl $PHP_VARIANTS \
 && phpbrew use $PHP_DIST_NAME \
 && which php \
 && php -v \
 && phpbrew info \
 && mkdir -p /src/php \
 && ln -s /root/.phpbrew/build/$PHPBREW_PHP /src/php/$PHPBREW_PHP

ENV PHPBREW_PHP=$PHP_DIST_NAME
ENV PATH=/root/.phpbrew/php/$PHP_DIST_NAME/bin:$PATH
