FROM ubuntu:18.04
ENV DEBIAN_FRONTEND=noninteractiv

WORKDIR /var/www

EXPOSE 80

CMD ["apachectl", "-D", "FOREGROUND"]

RUN apt-get update -y \
    && apt-get upgrade -y \
    && apt-get install -y software-properties-common \
    && add-apt-repository ppa:ondrej/php \
    && apt-get update -y && apt-get upgrade -y \
    && apt-get install -y \
    nano \
    git \
    curl \
    unzip \
    apache2 \
    php7.2 \
    libapache2-mod-php7.2 \
    php7.2-mysql \
    php7.2-sqlite \
    php7.2-xml \
    php7.2-gd \
    php7.2-zip \
    php7.2-mbstring \
    php7.2-json php7.2-curl \
    nodejs npm  \
    && apt-get -y autoremove \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* 

RUN /usr/sbin/a2enmod rewrite php7.2


RUN usermod -u 1000 www-data \
    && groupmod -g 1000 www-data \
    && /usr/bin/curl -sS https://getcomposer.org/installer | /usr/bin/php \
    && /bin/mv composer.phar /usr/local/bin/composer \
    && /bin/chown www-data:www-data -R /var/www

COPY 000-default.conf /etc/apache2/sites-available/



