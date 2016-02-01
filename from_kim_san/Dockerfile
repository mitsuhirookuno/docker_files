#
# Nginx Dockerfile
#
# https://github.com/dockerfile/nginx
#

# Pull base image.
FROM ubuntu:latest

# Install Nginx.
RUN \
  apt-get install -y software-properties-common && \
  add-apt-repository -y ppa:nginx/stable && \
  apt-get update && \
  apt-get install -y nginx && \
  rm -rf /var/lib/apt/lists/* && \
  echo "\ndaemon off;" >> /etc/nginx/nginx.conf && \
  chown -R www-data:www-data /var/lib/nginx

RUN apt-get update
RUN apt-get install -qq -y software-properties-common
RUN add-apt-repository -y ppa:nginx/stable
RUN echo "deb http://apt.postgresql.org/pub/repos/apt/ trusty-pgdg main" > /etc/apt/sources.list.d/pgdg.list && \
   apt-get update && \
   DEBIAN_FRONTEND=noninteractive \
   apt-get install -y --force-yes libpq-dev
RUN apt-get install -qq -y libmysqlclient-dev
RUN apt-get install -y vim mcrypt libmcrypt-dev locate man
#fapi
RUN apt-get install -y ImageMagick libmagickwand-dev

# Define mountable directories.
VOLUME ["/etc/nginx/sites-enabled", "/etc/nginx/certs", "/etc/nginx/conf.d", "/var/log/nginx", "/var/www/html"]

# Define working directory.
WORKDIR /etc/nginx

# Define default command.
CMD ["nginx"]

# Expose ports.
EXPOSE 80
EXPOSE 443
