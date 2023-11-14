FROM alpine:latest

RUN apk update \
    && apk upgrade \
    && apk add --no-cache nginx mc vim bash curl \
    && mkdir -p /www/val \
    && mkdir -p /run/nginx \
    && chown -R nginx:nginx /var/lib/nginx /www/val

COPY nginx.conf /etc/nginx/
COPY index.html /www/val/

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
