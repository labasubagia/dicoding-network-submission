FROM ubuntu:22.04

ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update -y
RUN apt-get install nodejs npm curl -y
RUN apt-get install apache2 libapache2-mod-evasive -y
RUN npm i -g pm2

WORKDIR /app
COPY  ./app .
RUN npm ci

COPY ./docker/apache2/apache2.conf /etc/apache2/apache2.conf
COPY ./docker/apache2/ports.conf /etc/apache2/ports.conf
COPY ./docker/apache2/000-default.conf /etc/apache2/sites-available/000-default.conf
COPY ./docker/apache2/evasive.conf /etc/apache2/mods-enabled/evasive.conf
RUN a2enmod proxy proxy_http evasive
# RUN a2enmod proxy proxy_http ratelimit
EXPOSE 3000

CMD service apache2 start && pm2-runtime npm -- start