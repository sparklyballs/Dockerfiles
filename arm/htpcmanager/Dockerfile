FROM container4armhf/armhf-alpine:3.3
MAINTAINER docker@libreelec.tv

ENV TZ="UTC"

# TZ is placeholder timezone setting so container will start if nothing is passed
# to overide, use either -e TZ="<your-timezone>" or map readonly to localtime on host.

# install build dependencies
RUN \
	apk add --update --virtual=build-dependencies \
	build-base \
	libffi-dev \
	linux-headers \
	openssl-dev \
	py-pip \
	python-dev \
	wget && \

# install pip packages
	pip install --no-cache-dir \
	cherrypy \
	psutil \
	pyopenssl && \

# clean up build dependencies
	apk del --purge build-dependencies && \

# install runtime dependencies
	apk add --update \
        git \
        py-paramiko \
        py-pillow \
        py-requests \
        tzdata && \

# cleanup
	rm -rf /var/cache/apk/* /root/.cache /tmp/*

# clone htpcmanager repository
RUN \
	git clone https://github.com/Hellowlol/HTPC-Manager /opt/htpcmanager


CMD ["/usr/bin/python", "/opt/htpcmanager/Htpc.py", "--datadir", "/config"]
EXPOSE 8085
VOLUME ["/config"]

