
FROM debian:latest

RUN apt-get update

RUN apt-get install -y wget apt-transport-https lsb-release ca-certificates

RUN wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg

RUN echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list

RUN apt-get update

RUN apt-get install -y apache2 htop mysql-client

RUN apt-get install -y php7.2-cgi php7.2-gd php7.2-curl php7.2-imap php7.2-sqlite3 php7.2-mysql php7.2-tidy php7.2-pspell php7.2-recode php7.2-xml php7.2-intl php7.2-enchant php7.2-gmp php7.2-mbstring php7.2-soap php7.2-xmlrpc php7.2-zip php7.2-fpm libapache2-mod-php7.2


# Manually set up the apache environment variables
ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2
ENV APACHE_LOCK_DIR /var/lock/apache2
ENV APACHE_PID_FILE /var/run/apache2.pid

# Expose apache.
EXPOSE 80

# Update the default apache site with the config we created.
ADD apache-config.conf /etc/apache2/sites-enabled/000-default.conf

RUN a2enmod rewrite

RUN rm -rf /var/log/apache2

RUN sed -i 's/33\:33/1000\:1000/g' /etc/passwd

CMD /usr/sbin/apache2ctl -D FOREGROUND
