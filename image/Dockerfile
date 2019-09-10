FROM alpine:3.7

# used https://www.fromlatest.io/#/ to reduce docker image size

ENV WORKDIR_FOLDER=/tmp/workdir
RUN mkdir -p $WORKDIR_FOLDER

RUN apk add --no-cache python3 \
 && python3 -m ensurepip \
 && pip3 install --upgrade pip setuptools \
 && rm -r /usr/lib/python*/ensurepip \
 && if [ ! -e /usr/bin/pip ]; then ln -s pip3 /usr/bin/pip ; fi \
 && if [[ ! -e /usr/bin/python ]]; then ln -sf /usr/bin/python3 /usr/bin/python; fi \
 && apk add --no-cache python3-dev \
### 3. Get ng-cli
 && apk add --no-cache --update nodejs \
 #update npm
 && npm i npm@latest -g \
 && npm install -g @angular/cli@7.3.9 \
### 4. install dependencies for eventlet, gevent, crypto
 && apk add --no-cache --virtual .build-deps gcc musl-dev libffi-dev libressl-dev\
 && pip install cython


WORKDIR $WORKDIR_FOLDER

COPY requirements.txt $WORKDIR_FOLDER
RUN pip install -r requirements.txt \
 && rm requirements.txt
