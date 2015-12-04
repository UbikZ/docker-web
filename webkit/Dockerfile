FROM debian
MAINTAINER UbikZ <gabriel.malet@gmail.com>

RUN apt-get update \
	&& apt-get install --no-install-recommends --yes \
		ca-certificates \
		openssh-client \
		curl \
		git \
		apache2 \
		php5 \
		php5-cli \
		php5-curl \
		php5-gd \
		php5-intl \
		php5-mysqlnd \
		php5-mcrypt \
		php5-apcu \
    nginx \
	&& apt-get clean \
	&& rm -rf /var/lib/apt/lists/*

# Apache
COPY config/apache/000-default.conf /etc/apache2/sites-available/000-default.conf
RUN a2enmod rewrite

# Nginx
COPY config/nginx/proxy_params /etc/nginx/proxy_params
COPY config/nginx/generic.conf /etc/nginx/sites-available/generic
RUN ln -s /etc/nginx/sites-available/generic /etc/nginx/sites-enabled/generic

# Composer
RUN curl -sS https://getcomposer.org/installer | php -- --filename=composer --install-dir=/usr/local/bin

# NodeJS
RUN curl -sL https://deb.nodesource.com/setup_5.x | bash - && apt-get install --yes nodejs

# Clean
RUN rm -rf /tmp/* /var/tmp/*

VOLUME /var/www/html
EXPOSE 80

COPY scripts/entrypoint.sh /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]

CMD ["apache2", "nginx", "-D", "FOREGROUND"]
