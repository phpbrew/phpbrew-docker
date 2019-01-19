FROM ubuntu:18.04

LABEL MAINTAINER "Yo-An Lin <yoanlin93@gmail.com>"

RUN apt-get update

RUN apt-get install -y --no-install-recommends \
        # phpbrew used tools
        curl git \
        # build tools
        build-essential bison autoconf automake autotools-dev re2c \
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
        mysql-server mysql-client libmysqlclient-dev libmysqld-dev
        # postgresql extension \
        postgresql postgresql-client postgresql-contrib
