FROM ubuntu:22.04
RUN apt-get update \
    && apt-get install apache2 -y \
    && apt clean
COPY index.html /var/www/html/index.html
EXPOSE 80
CMD ["apache2ctl", "-D", "FOREGROUND"]