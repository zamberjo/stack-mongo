FROM arm32v7/debian:jessie-slim

# https://andyfelong.com/2017/03/mongodb-3-0-14-binaries-for-raspberry-pi-3/
ARG CORE_URL="https://andyfelong.com/downloads/core_mongodb_3_0_14.tar.gz"
ARG CORE_MD5="46bf23049406f02f5379d1d286a5e4f3"
ARG TOOLS_URL="https://andyfelong.com/downloads/tools_mongodb_3_0_14.tar.gz"
ARG TOOLS_MD5="bc1ca8c3346758e338e0490548c6567e"

RUN set -ex \
    && export DEBIAN_FRONTEND=noninteractive \
    && apt-get update \
    && apt-get install --yes --no-install-recommends \
        wget ca-certificates \
    && wget -O /tmp/core_mongodb.tar.gz --quiet "${CORE_URL}" \
    && echo "${CORE_MD5}  /tmp/core_mongodb.tar.gz" | md5sum -c \
    && tar xzvf /tmp/core_mongodb.tar.gz -C /usr/local/bin/ \
    && wget -O /tmp/tools_mongodb.tar.gz --quiet "${TOOLS_URL}" \
    && echo "${TOOLS_MD5}  /tmp/tools_mongodb.tar.gz" | md5sum -c \
    && tar xzvf /tmp/tools_mongodb.tar.gz -C /usr/local/bin/ \
    && adduser \
        --ingroup nogroup \
        --shell /etc/false \
        --disabled-password \
        --gecos '' \
        --no-create-home \
        mongodb \
    && mkdir -p /data/db \
    && chown mongodb. /data/db \
    && apt-get remove --yes --purge \
        wget ca-certificates \
    && rm -rf \
        /tmp/core_mongodb.tar.gz \
        /var/lib/apt/lists/*

USER mongodb
VOLUME /data/db

EXPOSE 27017
ENTRYPOINT ["/usr/local/bin/mongod"]
