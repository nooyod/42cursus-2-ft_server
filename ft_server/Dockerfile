# **************************************************************************** #
#                                                                              #
#                                                         :::      ::::::::    #
#    Dockerfile                                         :+:      :+:    :+:    #
#                                                     +:+ +:+         +:+      #
#    By: doyokim <doyokim@student.42.fr>            +#+  +:+       +#+         #
#                                                 +#+#+#+#+#+   +#+            #
#    Created: 2021/04/27 15:14:43 by doyokim           #+#    #+#              #
#    Updated: 2021/04/28 15:02:40 by doyokim          ###   ########.fr        #
#                                                                              #
# **************************************************************************** #

FROM debian:buster

ENV DEBCONF_NOWARNINGS yes

RUN apt-get update &&  apt-get install -y \
	nginx \
	openssl \
	vim \
	wget \
	php-fpm \
	mariadb-server php-mysql

RUN openssl req -newkey rsa:4096 -days 365 -nodes -x509 -subj "/C=KR/ST=Seoul/L=Seoul/O=42Seoul/OU=Gon/CN=localhost" -keyout localhost.dev.key -out localhost.dev.crt

ADD ./srcs/phpMyAdmin-5.0.2-all-languages.tar.gz ./tmp
RUN mv ./tmp/phpMyAdmin-5.0.2-all-languages ./var/www/html/phpmyadmin

#CMD bash run.sh
