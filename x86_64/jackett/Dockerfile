FROM alpine:3.3
MAINTAINER docker@libreelec.tv

ENV HOME="/config"
ARG JACKETT_VER="v0.7.237"

# install dependencies
RUN apk add --no-cache libcurl --repository http://nl.alpinelinux.org/alpine/edge/main && \
apk add --no-cache --virtual=build-dependencies tar wget && \
apk add --no-cache mono --repository http://nl.alpinelinux.org/alpine/edge/testing && \

# install jackett from git
wget -O /tmp/jacket.tar.gz --no-check-certificate \
https://github.com/Jackett/Jackett/releases/download/${JACKETT_VER}/Jackett.Binaries.Mono.tar.gz && \
mkdir -p /opt/Jackett && \
tar xvf /tmp/jacket.tar.gz -C /opt/Jackett --strip-components=1 && \
apk del --purge build-dependencies && \
rm -rfv /var/cache/apk/* /tmp/*

EXPOSE 9117
VOLUME ["/config/.config/Jackett" "/downloads"]
CMD ["mono", "/opt/Jackett/JackettConsole.exe"]
