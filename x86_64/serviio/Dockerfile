FROM alpine:3.3
MAINTAINER docker@libreelec.tv

ARG SERVIIO_VER="1.6.1"
ENV HOME="/config/serviio"

# install dependencies
RUN \
apk add --no-cache \
	ffmpeg \
	openjdk8-jre \
	tar && \
rm -rfv /var/cache/apk/* /tmp/*

# fetch serviio
RUN \
	wget -O /tmp/serviio.tar.gz \
	http://download.serviio.org/releases/serviio-${SERVIIO_VER}-linux.tar.gz && \

# unpack serviio files, create some folders and copy default config for runtime
	mkdir -p \
		/app/serviio \
		/config/serviio/config \
		/config/serviio/library && \
	tar xvf /tmp/serviio.tar.gz -C /app/serviio --strip-components=1 && \
	cp /app/serviio/config/* /config/serviio/config/ && \

# cleanup
	rm -rfv /tmp/*


CMD ["/usr/bin/java", "-Xmx512M", "-Xms20M", "-XX:+UseG1GC", "-XX:GCTimeRatio=1", \
"-XX:MinHeapFreeRatio=10", "-XX:MaxHeapFreeRatio=20", "-Djava.net.preferIPv4Stack=true", \
"-Djava.awt.headless=true", "-Dorg.restlet.engine.loggerFacadeClass=org.restlet.ext.slf4j.Slf4jLoggerFacade", \
"-Dderby.system.home=/config/serviio/library", "-Dserviio.home=/app/serviio", \
"-Dplugins.location=/config/serviio", "-Dserviio.defaultTranscodeFolder=/transcode", \
"-Dffmpeg.location=ffmpeg", "-classpath", "/app/serviio/lib/*:/config/serviio/config", \
"org.serviio.MediaServer"]

# ports and volumes
EXPOSE 23423/tcp 23424/tcp 8895/tcp 1900/udp
VOLUME ["/config" "/transcode" "/media"]

