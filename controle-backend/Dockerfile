FROM php:8.2-apache

# Instala dependências do sistema e a extensão do PostgreSQL
RUN apt-get update && apt-get install -y \
    libpq-dev \
    && docker-php-ext-install pdo_pgsql

# Habilita o mod_rewrite
RUN a2enmod rewrite

# Copia o arquivo de configuração
COPY 000-default.conf /etc/apache2/sites-available/000-default.conf

WORKDIR /var/www/html

# Copia o código
COPY . /var/www/html

# Ajusta permissões
RUN chown -R www-data:www-data /var/www/html
RUN chmod -R 775 /var/www/html

RUN a2ensite 000-default.conf

EXPOSE 80

# Ajusta permissões de storage e cache
RUN chown -R www-data:www-data /var/www/html/storage /var/www/html/bootstrap/cache
RUN chmod -R 775 /var/www/html/storage /var/www/html/bootstrap/cache
