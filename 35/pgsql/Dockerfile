FROM php:7.2-apache

WORKDIR /root

RUN curl -L https://download.moodle.org/download.php/direct/stable35/moodle-latest-35.tgz > ./moodle.tgz
RUN tar -xvzf ./moodle.tgz -C /var/www/html/ \
    && mv /var/www/html/moodle/* /var/www/html/ \
    && mv /var/www/html/moodle/.[!.]* /var/www/html/
RUN mkdir /var/www/moodledata && chmod -R 0777 /var/www/moodledata
RUN rmdir /var/www/html/moodle && rm ./moodle.tgz

COPY ./moodle-devmode /usr/local/bin/moodle-devmode
COPY ./moodle-prodmode /usr/local/bin/moodle-prodmode
RUN chmod 0775 /usr/local/bin/moodle-devmode && chmod 0775 /usr/local/bin/moodle-prodmode

WORKDIR /var/www/html
RUN chmod -R 0777 /var/www/html

RUN apt-get update && apt-get install -y zlib1g-dev libpng-dev libicu-dev libxml2-dev libpq-dev
RUN docker-php-ext-install zip gd intl xmlrpc soap pgsql
RUN docker-php-ext-enable zip gd intl xmlrpc soap pgsql opcache
