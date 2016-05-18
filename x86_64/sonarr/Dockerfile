FROM alpine:3.3
MAINTAINER docker@libreelec.tv

ARG SONARR_VERSION="2.0.0.3953"

# install dependencies
RUN \
	apk add --update sqlite && \

	apk add mono libmediainfo --update-cache --repository \
	http://nl.alpinelinux.org/alpine/edge/testing && \

# cleanup
	rm -rf /var/cache/apk/*

# fetch sonarr
RUN \
	wget -O - http://download.sonarr.tv/v2/master/mono/NzbDrone.master.${SONARR_VERSION}.mono.tar.gz \
	| tar xzf -

# ports and volumes
EXPOSE 8989
VOLUME ["/config","/downloads","/media"]

CMD ["mono", "/NzbDrone/NzbDrone.exe", "--no-browser", "-data=/config"]

