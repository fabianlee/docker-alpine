# FAB default to apache version being used, override with --build-arg 
ARG ALPINE_BASE_VERSION=3.11.3
FROM fabianlee/alpine-base:$ALPINE_BASE_VERSION
MAINTAINER Scott Mebberson <scott@scottmebberson.com>

# Install apache
# can override with docker build: --build-arg APACHE2_VERSION="2.4.41-r0"
ARG APACHE2_VERSION=2.4.41-r0
RUN echo APACHE2_VERSION is ${APACHE2_VERSION} AND $APACHE2_VERSION \ 
	&& apk update \
	&& apk add --no-cache bind-tools cups-client apache2=${APACHE2_VERSION} apache2-utils=${APACHE2_VERSION}
RUN apk policy apache2 \
	&& apk policy apache2-utils

RUN mkdir -p /run/apache2/

# Add the files
ADD root /

# Expose the ports for apache
EXPOSE 80 443
