FROM php:7.1-apache
RUN apt-get update && apt-get install -y \
            git
RUN docker-php-ext-install \ 
            gettext \ 
            mysqli

RUN cd /var/www/html/ && git clone -b "v3.0.1" https://github.com/coral-erm/coral.git

RUN chmod 777 -R /var/www/html/coral/ 
RUN echo -e "DocumentRoot \"/web\" \nServerName localhost \nLoadModule mpm_event_module /usr/lib/apache2/mod_mpm_event.so \nListen 80" | tee /etc/apache2/httpd.conf

CMD apachectl -DFOREGROUND
