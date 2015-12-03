FROM debian
MAINTAINER UbikZ <gabriel.malet@gmail.com>

RUN apt-get update \
	&& apt-get install --no-install-recommends --yes \
		curl \
		nginx \
	&& apt-get clean \
	&& rm -rf /var/lib/apt/lists/*

# Nginx
COPY config/generic /etc/nginx/sites-available/generic.conf
COPY config/proxy_params /etc/nginx/proxy_params

# Clean
RUN rm -rf /tmp/* /var/tmp/*

EXPOSE 80

CMD ["service", "nginx", "start"]
