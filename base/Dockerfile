# This image is the base image for all OpenShift v3 language container images.
FROM hidevopsio/s2i-core-alpine

ENV SUMMARY="Base image with essential libraries and tools used as a base for \
builder images like perl, python, ruby, etc." \
    DESCRIPTION="The s2i-base image, being built upon s2i-core, provides any \
images layered on top of it with all the tools needed to use source-to-image \
functionality. Additionally, s2i-base also contains various libraries needed for \
it to serve as a base for other builder images, like s2i-python or s2i-ruby." 

LABEL summary="$SUMMARY" \
      description="$DESCRIPTION" \
      io.k8s.description="$DESCRIPTION" \
      io.k8s.display-name="s2i base" \
      com.redhat.component="s2i-base-docker" \
      name="hidevopsio/s2i-base-alpine" \
      version="1" \
      release="1" \
      maintainer="John Deng <john.deng@outlook.com>"

# This is the list of basic dependencies that all language container image can
# consume.
RUN INSTALL_PKGS="autoconf \
  automake \
  gcc \
  g++ \
  gdb \
  git \
  lsof \
  make \
  openssl \
  patch \
  procps \
  wget \
  curl \
  libcurl \
  libxml2-dev \
  libxslt-dev \
  openssl-dev \
  zlib-dev" && \
  apk add $INSTALL_PKGS

