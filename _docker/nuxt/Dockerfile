FROM node
ARG PROJECT_DIR
RUN apt-get update

WORKDIR /var/www/nuxt
COPY $PROJECT_DIR /var/www/nuxt
RUN npm install

RUN npm ci && npm cache clean --force
RUN npm run build

ENV HOST 0.0.0.0
EXPOSE 3000

# this NUXT-VERSION-3 works only with ENTRYPOINT
ENTRYPOINT ["node", ".output/server/index.mjs"]
