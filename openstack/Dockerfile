FROM alpine:latest
RUN apk add --no-cache \
  python-dev \
  py-pip \
  py-setuptools \
  ca-certificates && \
  apk add --no-cache \
  --virtual build-deps \
  gcc \
  libffi-dev \
  openssl-dev \
  musl-dev \
  linux-headers \
  && pip install --upgrade --no-cache-dir pip setuptools python-openstackclient \
  && apk del build-deps \
  && rm -rf /var/cache/apk/*
