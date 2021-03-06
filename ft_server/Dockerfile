# **************************************************************************** #
#                                                                              #
#                                                         :::      ::::::::    #
#    Dockerfile                                         :+:      :+:    :+:    #
#                                                     +:+ +:+         +:+      #
#    By: doyokim <doyokim@student.42seoul.fr>       +#+  +:+       +#+         #
#                                                 +#+#+#+#+#+   +#+            #
#    Created: 2021/04/27 15:14:43 by doyokim           #+#    #+#              #
#    Updated: 2021/05/07 10:40:33 by doyokim          ###   ########.fr        #
#                                                                              #
# **************************************************************************** #

FROM debian:buster

ENV DEBCONF_NOWARNINGS yes

RUN apt-get update && apt-get install -y \
	nginx \
	openssl \
	vim \
	wget \
	php-fpm \
	mariadb-server php-mysql

RUN openssl req -newkey rsa:4096 -days 365 -nodes -x509 -subj "/C=KR/ST=Seoul/L=Seoul/O=42Seoul/OU=Gon/CN=localhost" -keyout localhost.dev.key -out localhost.dev.crt && mv localhost.dev.key ./etc/ssl/private/ && mv localhost.dev.crt ./etc/ssl/certs/ && chmod 600 etc/ssl/certs/localhost.dev.crt etc/ssl/private/localhost.dev.key

ADD ./srcs/phpMyAdmin-5.0.2-all-languages.tar.gz .
RUN mv phpMyAdmin-5.0.2-all-languages ./var/www/html/phpmyadmin

COPY ./srcs/default ./etc/nginx/sites-available/

RUN ./etc/init.d/mysql start && mysql -u root -e "CREATE DATABASE wordpress;" --skip-password && mysql -u root -e "CREATE USER 'doyokim'@'localhost' IDENTIFIED BY '1234';" --skip-password && mysql -u root -e "GRANT ALL PRIVILEGES ON wordpress.* TO 'doyokim'@'localhost' WITH GRANT OPTION;" --skip-password

ADD ./srcs/wordpress-5.7.1.tar.gz .
RUN	mv wordpress ./var/www/html/
RUN chown -R www-data:www-data /var/www/html/wordpress

COPY ./srcs/wp-config.php ./var/www/html/wordpress/
COPY ./srcs/config.inc.php ./var/www/html/phpmyadmin/

EXPOSE 80 443

ENTRYPOINT service nginx start && service php7.3-fpm start && service mysql start && /bin/bash
