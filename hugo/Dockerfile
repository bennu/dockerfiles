FROM golang:1.11-alpine3.8 AS build
ARG RELEASE
ENV RELEASE=${RELEASE:-master}
RUN apk add --no-cache git musl-dev && \
	go get -v github.com/gohugoio/hugo && \
    cd /go/src/github.com/gohugoio/hugo && \
    git checkout ${RELEASE} && \
    CGO_ENABLED=0 GOOS=linux go build -a -ldflags="-s -w" -installsuffix cgo && \
    echo "http://dl-cdn.alpinelinux.org/alpine/edge/main" >> /etc/apk/repositories && \
    echo "http://dl-cdn.alpinelinux.org/alpine/edge/community" >> /etc/apk/repositories && \
    echo "http://dl-cdn.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories && \
    apk add --no-cache upx && \
    upx --best hugo

FROM scratch
COPY --from=build /go/src/github.com/gohugoio/hugo/hugo /usr/local/bin/hugo
ENTRYPOINT [ "/usr/local/bin/hugo" ]
