FROM node:12.16.3-stretch-slim

MAINTAINER Halil Tuncay Uner <tuncay@digitalact.com.tr>

ARG UID
ARG GID

RUN usermod -u $UID node
RUN groupmod -g $GID node

USER node

WORKDIR /home/node/project
