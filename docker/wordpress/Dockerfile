FROM wordpress:6.9.4-php8.3-apache

RUN apt-get update && apt-get purge -y \
    listen \
    ncat \
    curl \
    && apt-get autoremove -y && apt-get clean && rm -rf /var/lib/apt/lists/*

RUN sed -i 's/Listen 80/Listen 8080/g' /etc/apache2/ports.conf \
    && sed -i 's/<VirtualHost \*:80>/<VirtualHost \*:8080>/g' /etc/apache2/sites-available/000-default.conf

RUN sed -i '/<Directory \/var\/www\/>/,/<\/Directory>/s/AllowOverride None/AllowOverride All/' /etc/apache2/apache2.conf

RUN chown -R www-data:www-data /var/www/html

COPY security.conf /etc/apache2/conf-available/security.conf

RUN a2enconf security && a2enmod rewrite

RUN echo "expose_php = Off" > /usr/local/etc/php/conf.d/security.ini

USER www-data
