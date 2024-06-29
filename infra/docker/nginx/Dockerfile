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

# nginx config file
COPY ./infra/docker/nginx/*.conf /etc/nginx/conf.d/

WORKDIR /work/backend
