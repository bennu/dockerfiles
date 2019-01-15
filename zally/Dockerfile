FROM golang:1.11-alpine3.8 AS base
RUN apk add --no-cache \
	git \
	upx && \
    go get -v -u github.com/golang/dep/cmd/dep

FROM base AS build
WORKDIR /go/src/github.com/zalando
RUN git clone https://github.com/zalando/zally.git && \
    cd zally/cli/zally && \
    dep ensure && \
    CGO_ENABLED=0 GOOS=linux go build -a -ldflags="-s -w" -installsuffix cgo && \
    upx --best zally && \
    mv zally /usr/local/bin/zally

FROM scratch
COPY --from=build /usr/local/bin/zally /zally
ENTRYPOINT [ "/zally" ]
