FROM node:14.11-buster-slim
ARG PROJECT_DIR
RUN apt-get update

WORKDIR /var/www/nuxt
RUN npm install
COPY $PROJECT_DIR /var/www/nuxt

RUN npm ci
RUN npm run build

ENV HOST 0.0.0.0
