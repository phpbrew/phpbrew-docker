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
