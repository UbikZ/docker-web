FROM debian
MAINTAINER UbikZ <gabriel.malet@gmail.com>

RUN apt-get update \
	&& apt-get install --no-install-recommends --yes \
		curl \
		apache2 \
		php5 \
		php5-cli \
		php5-curl \
		php5-intl \
		php5-mcrypt \
	&& apt-get clean \
	&& rm -rf /var/lib/apt/lists/*

# Apache
RUN a2enmod rewrite

# Composer
RUN curl -sS https://getcomposer.org/installer | php -- --filename=composer --install-dir=/usr/local/bin

# Clean
RUN rm -rf /tmp/* /var/tmp/*

EXPOSE 80

CMD ["service", "apache2", "start"]
