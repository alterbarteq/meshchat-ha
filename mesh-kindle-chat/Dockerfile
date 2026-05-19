ARG BUILD_FROM=ghcr.io/home-assistant/amd64-base:3.19
FROM $BUILD_FROM

RUN apk add --no-cache busybox-extras

COPY rootfs /
COPY index.html /var/www/index.html

EXPOSE 8765
