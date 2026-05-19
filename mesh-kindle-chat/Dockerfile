ARG BUILD_FROM
FROM $BUILD_FROM

RUN apk add --no-cache busybox-extras

COPY rootfs /
COPY index.html /var/www/index.html

EXPOSE 8765
