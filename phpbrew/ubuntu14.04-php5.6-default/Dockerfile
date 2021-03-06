FROM  ubuntu:14.04
# FROM  debian:jessie

MAINTAINER Yo-An Lin "yoanlin93@gmail.com"

USER root

ENV DEBIAN_FRONTEND noninteractive

ENV PHP_VERSION 5.6

ENV PHP_SUBVERSION $PHP_VERSION.10

ENV PHPBREW_ROOT /root/.phpbrew

ENV PHPBREW_HOME /root/.phpbrew

ENV PHPBREW_PHP php-$PHP_VERSION.10

ENV PHPBREW_SET_PROMPT 1


SHELL ["/bin/bash", "-c"]

RUN echo "Asia/Taipei" > /etc/timezone && dpkg-reconfigure -f noninteractive tzdata

RUN perl -i.bak -pe "s/archive.ubuntu.com/free.nchc.org.tw/g" /etc/apt/sources.list

ENV DEBIAN_FRONTEND="noninteractive"

RUN apt-get update \
  && apt-get -qqy install php5 \
  && apt-get -qqy install php5-dev \
  && apt-get -qqy install php5-cli \
  && apt-get -qqy install php-apc \
  && apt-get -qqy install php-pear \
  && apt-get -qqy install php5-curl \
  && apt-get -qqy install php5-fpm \
  && apt-get -qqy install php5-gd \
  && apt-get -qqy install php5-mysql \
  && apt-get -qqy install php5-xdebug \
  && apt-get -qqy install autoconf automake curl build-essential libxslt1-dev re2c libxml2 libxml2-dev php5-cli bison libbz2-dev libreadline-dev \
  && apt-get -qqy install libfreetype6 libfreetype6-dev libpng12-0 libpng12-dev libjpeg-dev libjpeg8-dev libjpeg8 libgd-dev libgd3 libxpm4 libltdl7 libltdl-dev \
  && apt-get -qqy install libssl-dev openssl \
  && apt-get -qqy install gettext libgettextpo-dev libgettextpo0 \
  && apt-get -qqy install libicu-dev \
  && apt-get -qqy install libmhash-dev libmhash2 \
  && apt-get -qqy install libmcrypt-dev libmcrypt4 \
  && apt-get -qqy install mysql-client libmysqlclient-dev libmysqld-dev \
  && apt-get -qqy install ca-certificates \
  && apt-get -qqy install libyaml-dev libyaml-0-2 \
  && apt-get -qqy install libcurl4-gnutls-dev libexpat1-dev libz-dev librecode0 \
  && apt-get -qqy install libpcre3-dev libpcre++-dev \
  && apt-get -qqy install git \
  && apt-get -qqy install wget \
  && apt-get -qqy install curl \
  && apt-get -qqy install sqlite3 \
  && apt-get clean -y \
  && apt-get autoclean -y \
  && apt-get autoremove -y \
  && rm -rf /var/lib/{apt,dpkg,cache,log}/ \
  && rm -rf /var/lib/apt/lists/*

# Install php tools
RUN mkdir -p /usr/bin \
  && wget -q -O /usr/bin/phpunit https://phar.phpunit.de/phpunit.phar && chmod +x /usr/bin/phpunit \
  && wget -q -O /usr/bin/composer https://getcomposer.org/composer.phar && chmod +x /usr/bin/composer \
  && wget -q -O /usr/bin/phpmd http://static.phpmd.org/php/latest/phpmd.phar && chmod +x /usr/bin/phpmd \
  && wget -q -O /usr/bin/sami http://get.sensiolabs.org/sami.phar && chmod +x /usr/bin/sami \
  && wget -q -O /usr/bin/phpcov https://phar.phpunit.de/phpcov.phar && chmod +x /usr/bin/phpcov \
  && wget -q -O /usr/bin/phpcpd https://phar.phpunit.de/phpcpd.phar && chmod +x /usr/bin/phpcpd \
  && wget -q -O /usr/bin/phploc https://phar.phpunit.de/phploc.phar && chmod +x /usr/bin/phploc \
  && wget -q -O /usr/bin/phptok https://phar.phpunit.de/phptok.phar && chmod +x /usr/bin/phptok \
  && wget -q -O /usr/bin/box https://github.com/box-project/box2/releases/download/2.5.2/box-2.5.2.phar && chmod +x /usr/bin/box \
  && wget -q -O /usr/bin/phpbrew https://github.com/phpbrew/phpbrew/raw/master/phpbrew && chmod +x /usr/bin/phpbrew

SHELL ["/bin/bash", "-c"]

RUN phpbrew init \
  && echo 'source $HOME/.phpbrew/bashrc' >> /root/.bashrc \
  && source ~/.phpbrew/bashrc \
  && phpbrew install --downloader wget --mirror http://us1.php.net $PHP_SUBVERSION \
              +default +bcmath +bz2 +calendar +cli +ctype +dom +fileinfo +filter +json \
              +mbregex +mbstring +mhash +pcntl +pcre +pdo +phar +posix +readline +sockets \
              +tokenizer +xml +curl +zip +openssl=yes +icu +opcache +fpm +sqlite +mysql +icu +default +intl +gettext

ENV DEBIAN_FRONTEND "noninteractive"

ENV TZ "Asia/Taipei"
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

WORKDIR /home/ubuntu
COPY entrypoint.sh /entrypoint.sh
ENTRYPOINT ["entrypoint.sh"]
