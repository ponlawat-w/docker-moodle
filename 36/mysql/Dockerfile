FROM php:7.2-apache

COPY ./moodle-devmode /usr/local/bin/moodle-devmode
COPY ./moodle-prodmode /usr/local/bin/moodle-prodmode
RUN chmod 0775 /usr/local/bin/moodle-devmode && chmod 0775 /usr/local/bin/moodle-prodmode

RUN apt-get update && apt-get install -y zlib1g-dev libpng-dev libicu-dev libxml2-dev
RUN docker-php-ext-install zip gd intl xmlrpc soap \
    && docker-php-ext-enable zip gd intl xmlrpc soap opcache

RUN curl -L https://download.moodle.org/download.php/direct/stable36/moodle-latest-36.tgz > ./moodle.tgz
RUN tar -xvzf ./moodle.tgz -C /var/www/html/ \
    && mv /var/www/html/moodle/* /var/www/html/ \
    && mv /var/www/html/moodle/.[!.]* /var/www/html/
RUN mkdir /var/www/moodledata && chmod -R 0777 /var/www/moodledata
RUN rmdir /var/www/html/moodle && rm ./moodle.tgz

RUN docker-php-ext-install mysqli && docker-php-ext-enable mysqli
WORKDIR /var/www/html

