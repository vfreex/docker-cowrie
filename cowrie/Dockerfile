FROM alpine:3.4
MAINTAINER Rayson Zhu <vfreex+docker@gmail.com>

WORKDIR /opt/cowrie/cowrie-master
EXPOSE 2222
CMD ["twistd", "-n", "-l", "log/cowrie.log", "--umask", "0077", "cowrie"]

RUN apk add --no-cache ca-certificates wget python py-pip py-twisted py-cryptography \
        py-openssl py-enum34 py-six py-asn1 py-ipaddress py-cffi py-idna && \
    pip install service_identity && \
    adduser -D cowrie && \
    wget -O /tmp/cowrie-master.zip https://github.com/micheloosterhof/cowrie/archive/master.zip && \
    mkdir -p /opt/cowrie && \
    unzip -d /opt/cowrie /tmp/cowrie-master.zip && \
    rm /tmp/cowrie-master.zip && \
    chown -R cowrie: /opt/cowrie && \
    cd /opt/cowrie/cowrie-master && \
    cp -a cowrie.cfg.dist cowrie.cfg && \
    apk del ca-certificates wget

