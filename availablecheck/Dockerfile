FROM alpine:latest
RUN apk add --no-cache bash curl
COPY availablecheck /bin/
ENTRYPOINT [ "/bin/bash" ]
CMD ["/bin/availablecheck"]
