FROM debian:buster

ENV DEBIAN_FRONTEND=noninteractive

# Basics
RUN apt-get update && apt-get install -y wget lsb-release

# Install PHP and the rest
# Debian Buster only has php-redis 4.2, we need 4.3
RUN wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg \
    && echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list \
    && apt-get update \
    && apt-get -y --no-install-recommends install \
        ca-certificates \
        curl \
        unzip \
        sudo \
        git \
        php-apcu \
        php-apcu-bc \
        php7.3-cli \
        php7.3-curl \
        php7.3-soap \
        php7.3-json \
        php7.3-mbstring \
        php7.3-opcache \
        php7.3-readline \
        php7.3-xml \
        php7.3-zip \
        php7.3-redis \
        php7.3-fpm \
        php7.3-ldap \
        php7.3-gmp \
        php7.3-xdebug \
        composer \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

STOPSIGNAL SIGQUIT

ARG UID
RUN useradd -u "$UID" -ms /bin/bash user
RUN echo 'user ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers
USER user

RUN git config --global url."https://gitlab.tugraz.at/".insteadOf "git@gitlab.tugraz.at:"

CMD ["/usr/sbin/php-fpm7.3", "-O" ]
EXPOSE 9000
WORKDIR "/application"