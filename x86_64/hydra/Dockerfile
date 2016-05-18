FROM libreelec/python:1.0.1
MAINTAINER docker@libreelec.tv

ARG HYDRA_VER="0.0.1a90"

# install nzbhydra
RUN \
	wget -O - https://github.com/theotherp/nzbhydra/archive/${HYDRA_VER}.tar.gz | tar xzf - && \
	mv /nzbhydra-${HYDRA_VER}  /NzbHydra

EXPOSE 5075
VOLUME ["/config"]

CMD ["/usr/bin/python", "/NzbHydra/nzbhydra.py", "--config /config/nzbhydra.conf", \
"--database /config/nzbhydra.db", "--logfile /config/nzbhydra.log", "--nobrowser"]


