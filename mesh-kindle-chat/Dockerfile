FROM alpine:3.19

RUN apk add --no-cache busybox-extras

COPY index.html /var/www/index.html

EXPOSE 8765

CMD ["httpd", "-f", "-p", "8765", "-h", "/var/www"]
