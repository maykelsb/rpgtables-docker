FROM php:7.1-apache

# Atualizando pacotes e instalando utilitarios
RUN apt-get update && apt-get install -y git unzip

# Instalando o composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN composer --version

# Ajustando o timezone
RUN rm /etc/localtime
RUN ln -s /usr/share/zoneinfo/America/Sao_Paulo /etc/localtime
RUN "date"

# Instalando pdo e pdo_mysql
RUN docker-php-ext-install pdo pdo_mysql

# Instalando o xdebug e configurando na porta 9001
RUN pecl install xdebug
RUN docker-php-ext-enable xdebug
RUN echo "error_reporting = E_ALL" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
RUN echo "display_startup_errors = On" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
RUN echo "display_errors = On" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
RUN echo "xdebug.remote_enable=1" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
RUN echo "xdebug.remote_connect_back=1" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
RUN echo "xdebug.idekey=\"XDEBUG\"" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
RUN echo "xdebug.remote_port=9001" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini

# Configurando vhost
RUN echo "<VirtualHost *:80>" >> /etc/apache2/sites-available/app.conf
RUN echo "    ServerName localdev" >> /etc/apache2/sites-available/app.conf
RUN echo "    ServerAlias localdev" >> /etc/apache2/sites-available/app.conf
RUN echo "    DocumentRoot /var/www/app/public" >> /etc/apache2/sites-available/app.conf
RUN echo "    <Directory \"/var/www/app/public\">" >> /etc/apache2/sites-available/app.conf
RUN echo "        AllowOverride All" >> /etc/apache2/sites-available/app.conf
RUN echo "        Require all granted" >> /etc/apache2/sites-available/app.conf
RUN echo "    </Directory>" >> /etc/apache2/sites-available/app.conf
RUN echo "</VirtualHost>" >> /etc/apache2/sites-available/app.conf

# Habilitando o vhost
RUN ln -s /etc/apache2/sites-available/app.conf /etc/apache2/sites-enabled/app.conf

WORKDIR /var/www/app

EXPOSE 9001
