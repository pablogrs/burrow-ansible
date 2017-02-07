FROM golang:alpine

MAINTAINER LinkedIn Burrow "https://github.com/linkedin/Burrow"

RUN apk add --update bash curl git
RUN apk add ca-certificates wget
RUN update-ca-certificates
RUN rm -rf /var/cache/apk/*

RUN curl -sSO https://raw.githubusercontent.com/pote/gpm/v1.4.0/bin/gpm && \
  chmod +x gpm && mv gpm /usr/local/bin

RUN go get github.com/linkedin/Burrow
WORKDIR $GOPATH/src/github.com/linkedin/Burrow
RUN gpm install
RUN http_proxy=http://web-proxy.corp.hpecorp.net:8080 go install

WORKDIR /var/tmp/burrow

CMD ["/go/bin/Burrow", "--config", "/etc/burrow/burrow.cfg"]
