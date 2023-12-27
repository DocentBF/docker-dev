FROM debian:12-slim

ARG USER_ID
ARG GROUP_ID

# update

RUN apt-get update && apt-get -y upgrade

# install requirements, add Ondrej Sury's php repo

RUN apt-get install -y software-properties-common \
    build-essential \
    locales \
    unzip \
    sudo \
    wget \
    curl \
    git \
    cron && \
    apt-get -y install apt-transport-https lsb-release ca-certificates && \
    wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg && \
    sh -c 'echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list' && \
    apt-get update

# install php with dependencies

RUN apt-get install -y \
    php7.4-bcmath \
    php7.4-bz2 \
    php7.4-cli \
    php7.4-curl \
    php7.4-fpm \
    php7.4-gd \
    php7.4-intl \
    php7.4-imagick \
    php-json \
    php7.4-mbstring \
    php7.4-memcached \
    php7.4-mysql \
    php7.4-opcache \
    php7.4-redis \
    php7.4-soap \
    php7.4-xml \
    php7.4-zip \
    php7.4-xdebug  #dev

# install composer

RUN wget https://getcomposer.org/installer -O - -q \
    | php -- --install-dir=/bin --filename=composer --quiet

ENV COMPOSER_ALLOW_SUPERUSER 1

# MODIFY DEFAULTS
RUN mv /etc/php/7.4/fpm/pool.d/www.conf /etc/php/7.4/fpm/pool.d/www.conf.example && \
    mv /etc/php/7.4/fpm/php-fpm.conf /etc/php/7.4/fpm/php-fpm.conf.example
COPY ./php-fpm.conf /etc/php/7.4/fpm/php-fpm.conf

# ALLOW LOCAL USER MANAGE SERVICES
RUN echo "www-data ALL = NOPASSWD:/usr/sbin/php-fpm7.4" > "/etc/sudoers.d/www-data"

# create local user
# avoid using usermod! use useradd with '-l'
RUN userdel www-data && useradd -l -u ${USER_ID} www-data && groupmod -g ${GROUP_ID} www-data

WORKDIR /var/www

# copy entrypoint
COPY ./entrypoint.sh /entrypoint.sh

USER "${USER_ID}:${GROUP_ID}"

# run 
CMD ["/bin/sh", "/entrypoint.sh"]