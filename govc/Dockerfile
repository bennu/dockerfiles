FROM golang:alpine3.7
ARG RELEASE
ENV RELEASE=${RELEASE:-master}
RUN apk add --no-cache git && \
    go get -v github.com/vmware/govmomi/govc && \
    cd /go/src/github.com/vmware/govmomi/govc && \
    git checkout ${RELEASE} && \
    CGO_ENABLED=0 GOOS=linux go build -a -ldflags="-s -w" -installsuffix cgo && \
    echo "http://dl-cdn.alpinelinux.org/alpine/edge/main" >> /etc/apk/repositories && \
    echo "http://dl-cdn.alpinelinux.org/alpine/edge/community" >> /etc/apk/repositories && \
    echo "http://dl-cdn.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories && \
    apk add --no-cache upx && \
    upx --best govc

FROM alpine:3.7
COPY --from=0 /go/src/github.com/vmware/govmomi/govc/govc /usr/local/bin/govc
RUN apk add --no-cache ca-certificate
ENTRYPOINT [ "/usr/local/bin/govc" ]
