FROM node:buster-slim

ARG HUGO_VERSION=0.59.1

RUN mkdir -p /tmp/hugo &&  \
	cd /tmp/hugo && \
	curl -LO https://github.com/gohugoio/hugo/releases/download/v${HUGO_VERSION}/hugo_extended_${HUGO_VERSION}_Linux-64bit.tar.gz && \
	tar zxvf hugo_extended_0.59.1_Linux-64bit.tar.gz && \
	mv hugo /usr/local/bin && \
	npm install -D --save autoprefixer && \
	npm install -D --save postcss-cli && \
	apt update && apt install -y --no-install-recommends \
	git && \
	rm -rf /var/lib/apt/lists/* && \
	rm -rf /tmp/hugo

WORKDIR /site

EXPOSE 1313

ENTRYPOINT ["hugo"]
CMD ["--help"]
