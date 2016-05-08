FROM alpine:3.3
MAINTAINER docker@libreelec.tv

# install dependencies
RUN apk add --update sqlite && \
apk add mono libmediainfo --update-cache --repository http://nl.alpinelinux.org/alpine/edge/testing && \
rm -rf /var/cache/apk/*

# fetch sonarr
RUN wget -O - http://update.sonarr.tv/v2/master/mono/NzbDrone.master.tar.gz | tar xzf -

# ports and volumes
EXPOSE 8989
VOLUME ["/config","/downloads","/media"]

CMD ["mono", "/NzbDrone/NzbDrone.exe", "--no-browser", "-data=/config"]

