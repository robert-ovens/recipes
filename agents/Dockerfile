FROM gliderlabs/alpine:3.6
MAINTAINER robert.ovens@gmail.com
LABEL version "1.1.0"

ENV S3_TMP /tmp/s3cmd.zip
ENV S3_ZIP /tmp/s3cmd-master
ENV HUGO_VERSION 0.25

WORKDIR /tmp

RUN apk --no-cache add \
      bash \
      curl \
      git \
      jq \
      py-pip \
      python &&\
    pip install --upgrade \
      pip \
      python-dateutil &&\
    curl -sSL --output ${S3_TMP} https://github.com/s3tools/s3cmd/archive/master.zip &&\
    unzip -q ${S3_TMP} -d /tmp &&\
    mv ${S3_ZIP}/S3 ${S3_ZIP}/s3cmd /usr/bin/ &&\
    rm -rf /tmp/* &&\
    mkdir ~/.aws


# Install HUGO
RUN set -x && \
  apk add --update wget ca-certificates && \
  wget https://github.com/gohugoio/hugo/releases/download/v${HUGO_VERSION}/hugo_${HUGO_VERSION}_Linux-64bit.tar.gz && \
  tar xzf hugo_${HUGO_VERSION}_Linux-64bit.tar.gz && \
  rm -r hugo_${HUGO_VERSION}_Linux-64bit.tar.gz && \
  mv hugo /usr/bin/hugo && \
  apk del wget ca-certificates && \
  rm /var/cache/apk/*
