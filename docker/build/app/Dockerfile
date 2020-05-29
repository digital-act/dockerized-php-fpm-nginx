FROM debian:10-slim

MAINTAINER Halil Tuncay Uner <tuncay@digitalact.com.tr>

ARG UID
ARG GID

# UPGRADE PACKAGES
RUN apt-get update && \
    apt-get -y upgrade

# INSTALL PREREQUISITES
RUN apt-get install -y software-properties-common \
    build-essential \
    locales \
    unzip \
    sudo \
    wget \
    curl \
    git \
    cron

# PHP REPOSITORY
RUN apt-get -y install apt-transport-https lsb-release ca-certificates && \
    wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg && \
    sh -c 'echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list'

# UPDATE PACKAGE INDEX
RUN apt-get update

# INSTALL PHP
RUN apt-get install -y php7.4-fpm \
    php7.4-gd \
    php7.4-zip \
    php7.4-xml \
    php7.4-intl \
    php7.4-curl \
    php7.4-mbstring \
    php7.4-pdo-mysql \
    php-bcmath \
    php-redis

# INSTALL NGINX
RUN apt-get install -y nginx

# INSTALL COMPOSER
RUN curl --silent https://getcomposer.org/download/1.10.6/composer.phar -o /usr/local/bin/composer
RUN chmod +x /usr/local/bin/composer

# CREATE USER LOCAL USER
RUN useradd --shell /bin/bash --create-home dact
RUN usermod -u $UID dact
RUN groupmod -g $GID dact

# CREATE FOLDERS
RUN runuser -l dact -c 'mkdir log'

# MODIFY DEFAULTS
RUN rm /etc/nginx/sites-enabled/default && \
    mv /etc/php/7.4/fpm/pool.d/www.conf /etc/php/7.4/fpm/pool.d/www.conf.example

# ALLOW LOCAL USER MANAGE SERVICES
RUN echo "dact ALL = NOPASSWD:/usr/sbin/service,/usr/sbin/nginx" > "/etc/sudoers.d/dact"

# COPY ENTRYPOINT
COPY ./entrypoint.sh /home/dact/entrypoint.sh

# SET WORKING DIRECTORY
WORKDIR /home/dact/project

# SWITCH USER
USER dact

# COPY ENTRYPOINT
COPY ./entrypoint.sh /home/dact/entrypoint.sh

# SET ENTRYPOINT
CMD ["/bin/sh", "/home/dact/entrypoint.sh"]
