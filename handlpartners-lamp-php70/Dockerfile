FROM ubuntu:latest
MAINTAINER Matt Johnson <mjohnson@handlpartners.com>

# Setup Environment
ENV DEBIAN_FRONTEND noninteractive

# Update Sources
RUN apt-get update -y

# Install Apache
RUN apt-get install -y apache2 libapache2-mod-php
RUN mkdir -p /var/lock/apache2 /var/run/apache2
RUN rm -rf /var/www/html && mkdir /var/www/html
RUN a2enmod rewrite

# Install MySQL and bind to 0.0.0.0
RUN apt-get install -y mysql-client mysql-server
RUN sed -i -e"s/^bind-address\s*=\s*127.0.0.1/bind-address = 0.0.0.0/" /etc/mysql/mysql.conf.d/mysqld.cnf

# Install PHP 7
RUN apt-get install -y php php-common php-cli php-xml php-json php-mcrypt php-mbstring php-gd php-mysqlnd

# Install Supervisor
RUN apt-get install -y supervisor
RUN mkdir -p /var/log/supervisor

# Add volumes and configs
ADD supervisord.conf /etc/

# Expose ports and set launch script
EXPOSE 80 3306
CMD ["/usr/bin/supervisord"]
