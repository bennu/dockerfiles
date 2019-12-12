FROM alpine:latest
RUN apk add --no-cache \
  python-dev \
  py-pip \
  py-setuptools \
  jq \
  ca-certificates && \
  apk add --no-cache \
  --virtual build-deps \
  gcc \
  libffi-dev \
  openssl-dev \
  musl-dev \
  linux-headers \
  && pip install --upgrade --no-cache-dir \
  pip setuptools \
  # main official client
  python-openstackclient \
  # official clients per project (stable)
  python-glanceclient \
  python-ironicclient \
  python-manilaclient \
  python-novaclient \
  python-neutronclient \
  python-swiftclient \
  # official client per project (in development)
  python-barbicanclient \
  python-cinderclient \
  python-ceilometerclient \
  python-heatclient \
  python-troveclient \
  && apk del build-deps \
  && rm -rf /var/cache/apk/*
