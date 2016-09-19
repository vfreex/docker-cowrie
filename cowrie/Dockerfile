FROM alpine:3.4
MAINTAINER Rayson Zhu <vfreex+docker@gmail.com>

EXPOSE 2222
CMD ["twistd", "-n", "-l", "log/cowrie.log", "--umask", "0077", "cowrie"]

RUN apk add --no-cache ca-certificates wget python py-pip py-twisted py-cryptography \
        py-openssl py-enum34 py-six py-asn1 py-ipaddress py-cffi py-idna && \
    pip install service_identity && \
    adduser -D cowrie && \
    wget -O /tmp/cowrie.zip https://github.com/micheloosterhof/cowrie/archive/3d8085e86a13332311949e206c5a15b514db1d90.zip && \
    mkdir -p /opt && \
    unzip -d /opt /tmp/cowrie.zip && mv /opt/cowrie-* /opt/cowrie && \
    rm /tmp/cowrie.zip && \
    chown -R cowrie: /opt/cowrie && \
    cp -a /opt/cowrie/cowrie.cfg.dist /opt/cowrie/cowrie.cfg && \
    apk del ca-certificates wget

WORKDIR /opt/cowrie
