FROM alpine:latest

ADD 1.1-17.10.30-release.tar.gz /typecho/

RUN apk update \
    && apk add tzdata nginx php php-fpm php-pdo_sqlite php-ctype php-session php-tokenizer --no-cache \
    && cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
    && ln -sf /dev/stdout /var/log/nginx/access.log \
    && ln -sf /dev/stderr /var/log/nginx/error.log \
    && mkdir -p /run/nginx \
    && chown -R nobody. /typecho \
    && apk del tzdata \
    && rm -rf /var/cache/apk/* /tmp/*


COPY default.conf /etc/nginx/http.d/

VOLUME /typecho

EXPOSE 80/tcp

CMD ["sh", "-c", "php-fpm7 -F & nginx -g 'daemon off;'"]
