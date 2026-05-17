FROM wordpress:6.9.4-php8.3-apache

RUN apt-get update && apt-get purge -y \
    listen \
    ncat \
    curl \
    && apt-get autoremove -y && apt-get clean && rm -rf /var/lib/apt/lists/*

RUN sed -i 's/Listen 80/Listen 8080/g' /etc/apache2/ports.conf \
    && sed -i 's/<VirtualHost \*:80>/<VirtualHost \*:8080>/g' /etc/apache2/sites-available/000-default.conf

RUN chown -R www-data:www-data /var/www/html

COPY security.conf /etc/apache2/conf-available/security.conf

RUN a2enconf security && a2enmod rewrite

USER www-data
