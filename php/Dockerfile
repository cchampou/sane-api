# docker/php-fpm/Dockerfile

FROM php:7-fpm-alpine
COPY ./wait-for-it.sh /usr/bin/wait-for-it
RUN chmod +x /usr/bin/wait-for-it
RUN apk update
RUN apk --update --no-cache add git bash
RUN apk --no-cache add postgresql-dev
RUN docker-php-ext-install pdo_pgsql
COPY --from=composer /usr/bin/composer /usr/bin/composer
WORKDIR /var/www/sane
CMD composer install ; wait-for-it database:5432 -- php bin/console doctrine:schema:update --force ; php-fpm
ENV APP_ENV=production
EXPOSE 9000
