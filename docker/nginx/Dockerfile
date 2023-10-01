FROM ubuntu:22.04

ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update -y 
RUN apt-get install nodejs npm curl -y
RUN apt-get install nginx -y
RUN npm i -g pm2

WORKDIR /app
COPY  ./app .
RUN npm ci

COPY ./docker/nginx/default /etc/nginx/sites-available/default
EXPOSE 3000

CMD service nginx start && pm2-runtime npm -- start