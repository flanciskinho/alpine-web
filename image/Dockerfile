# syntax = docker/dockerfile:experimental

FROM python:3.7-alpine

# used https://www.fromlatest.io/#/ to reduce docker image size

# install dependences for python, C and heif support
### install dependencies for eventlet, gevent, crypto and python things
RUN apk add --no-cache libxml2 libxml2-dev libxslt-dev  \
 && apk add --no-cache --virtual .build-deps build-base linux-headers gcc musl-dev libffi-dev libressl-dev jpeg-dev zlib-dev openblas-dev lapack lapack-dev \
 && apk add --no-cache --update x265 libde265 libheif libheif-dev 

###  Get ng-cli
RUN apk add --no-cache --update nodejs npm \
 #update npm
 && npm i npm@latest -g \
 && npm install -g @angular/cli@7.3.9


RUN --mount=source=./,target=/tmp \
    pip install --no-cache-dir --upgrade pip \
 && pip install --no-cache-dir cython \
 && pip install --no-cache-dir -r /tmp/requirements.txt


