ARG BUILD_FROM=ghcr.io/home-assistant/amd64-base:3.19
FROM $BUILD_FROM

RUN apk add --no-cache busybox-extras

COPY index.html /var/www/index.html

CMD ["httpd", "-f", "-p", "8765", "-h", "/var/www"]
