FROM golang:alpine3.8
ARG RELEASE
ENV RELEASE=${RELEASE:-master}
RUN apk add --no-cache git && \
	go get -v github.com/kubernetes-sigs/kustomize && \
    cd /go/src/sigs.k8s.io/kustomize && \
    git checkout ${RELEASE} && \
    CGO_ENABLED=0 GOOS=linux go build -a -ldflags="-s -w" -installsuffix cgo && \
    echo "http://dl-cdn.alpinelinux.org/alpine/edge/main" >> /etc/apk/repositories && \
    echo "http://dl-cdn.alpinelinux.org/alpine/edge/community" >> /etc/apk/repositories && \
    echo "http://dl-cdn.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories && \
    apk add --no-cache upx && \
    upx --best kustomize

FROM scratch
COPY --from=0 /go/src/sigs.k8s.io/kustomize/kustomize /usr/local/bin/kustomize
ENTRYPOINT [ "/usr/local/bin/kustomize" ]
