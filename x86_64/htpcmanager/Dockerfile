FROM alpine:3.3
MAINTAINER docker@libreelec.tv

ENV TZ="UTC"

# TZ is placeholder timezone setting so container will start if nothing is passed
# to overide, use either -e TZ="<your-timezone>" or map readonly to localtime on host.

ARG APKLIST="git py-paramiko py-pillow py-requests tzdata"
ARG BUILD_LIST="build-base libffi-dev linux-headers openssl-dev py-pip python-dev wget"
ARG PIP_LIST="cherrypy psutil pyopenssl"

# install build dependencies and pip packages
RUN apk add --update $BUILD_LIST && \
pip install --no-cache-dir $PIP_LIST && \

# clean up build dependencies
apk del --purge $BUILD_LIST && \

# install runtime dependencies
apk add --update $APKLIST && \

# cleanup
rm -rf /var/cache/apk/* /root/.cache /tmp/*

# clone htpcmanager repository
RUN git clone https://github.com/Hellowlol/HTPC-Manager /opt/htpcmanager

CMD ["/usr/bin/python", "/opt/htpcmanager/Htpc.py", "--datadir", "/config"]
EXPOSE 8085
VOLUME ["/config"]
