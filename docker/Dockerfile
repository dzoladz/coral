FROM ubuntu:20.04

# ------------------------------------------------------------------
# Use BASH, not SH
# ------------------------------------------------------------------
SHELL ["/bin/bash", "-c"]

# ------------------------------------------------------------------
# Update Package Cache and Set Timezone
# ------------------------------------------------------------------
RUN apt-get update

RUN apt-get install -y tzdata
ENV TZ "America/New_York"
RUN echo "America/New_York" > /etc/timezone \
    && dpkg-reconfigure --frontend noninteractive tzdata

# ------------------------------------------------------------------
# Install Packages and Dependencies
# ------------------------------------------------------------------
RUN DEBIAN_FRONTEND='noninteractive' apt-get install -y --no-install-recommends \
    # -- General Utilities --
    git \
    nano \
    ca-certificates \
    # -- Apache --
    apache2 \
    libapache2-mod-php \
    # -- PHP | 20.04 repos point to 7.4 --
    php \
    php-gd \
    php-xml \
    php-zip \
    php-mysql \
    php-cli \
    php-curl \
    php-mbstring

# ------------------------------------------------------------------
# Copy PHP Configurations
# ------------------------------------------------------------------
COPY docker/php.ini /usr/local/etc/php/conf.d/

# ------------------------------------------------------------------
# Install Coral ERM
# ------------------------------------------------------------------
WORKDIR /var/www/html/
RUN git clone http://github.com/coral-erm/coral.git

RUN chmod 777 -R /var/www/html/coral/ && echo -e "DocumentRoot \"/web\" \nServerName localhost \nLoadModule mpm_event_module /usr/lib/apache2/mod_mpm_event.so \nListen 80" | tee /etc/apache2/httpd.conf
CMD apachectl -DFOREGROUND

# ------------------------------------------------------------------
# Expose Container Ports
# ------------------------------------------------------------------
EXPOSE 80
