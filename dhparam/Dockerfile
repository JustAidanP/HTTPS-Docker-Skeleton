FROM alpine:latest

WORKDIR /dhparam

RUN apk add openssl

CMD [ "openssl", "dhparam", "-out", "dhparam.pem", "2048" ]
