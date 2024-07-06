FROM nginx:1.20-alpine
LABEL maintainer="ucan-lab <yes@u-can.pro>"
SHELL ["/bin/ash", "-oeux", "pipefail", "-c"]

ENV TZ=UTC

RUN apk update && \
    apk add --update --no-cache \
    tzdata \
    curl \
    git \
    unzip \
    && \
    cp /usr/share/zoneinfo/UTC /etc/localtime && \
    apk del tzdata && \
    rm -rf /var/cache/apk/*

# node command
RUN apk add --update --no-cache nodejs
# npm command
RUN apk add --update --no-cache npm
# yarn command
RUN npm install -g yarn

# nginx config file will be output to /etc/nginx/conf.d/ by envsubst
COPY ./infra/docker/nginx/default.conf /etc/nginx/templates/default.conf.template
COPY ./infra/docker/nginx/nginx.conf /etc/nginx/nginx.conf

COPY ./backend/public /work/backend/public

WORKDIR /work/backend
