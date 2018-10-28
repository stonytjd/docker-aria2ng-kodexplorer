FROM abiosoft/caddy

WORKDIR /root

ENV RPC_SECRET=0123456789abcdef
ENV ENABLE_AUTH=true
ENV DOMAIN=:80
ENV ARIA2_USER=admin
ENV ARIA2_PWD=changeme

RUN apk update && apk add wget bash curl gnupg openrc screen aria2 tar --no-cache

ADD conf /root/conf

COPY Caddyfile /usr/local/caddy/Caddyfile
COPY SecureCaddyfile /usr/local/caddy/SecureCaddyfile

RUN mkdir -p /usr/local/www && mkdir -p /usr/local/www/aria2

#AriaNg
RUN mkdir /usr/local/www/aria2/Download && cd /usr/local/www/aria2 \
  && chmod +rw /root/conf/aria2.session \
  && wget -N --no-check-certificate https://github.com/mayswind/AriaNg/releases/download/0.4.0/aria-ng-0.4.0.zip && unzip aria-ng-0.4.0.zip && rm -rf aria-ng-0.4.0.zip \
  && chmod -R 755 /usr/local/www/aria2 \
  && chmod +x /root/conf/aria2c.sh

#The folder to store ssl keys
VOLUME /root/conf/key

EXPOSE 6800 80 443

ENTRYPOINT ["/bin/sh", "/root/conf/aria2c.sh"]
