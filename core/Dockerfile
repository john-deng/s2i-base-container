# This image is the base image for all s2i configurable container images.
FROM alpine:3.6

ENV SUMMARY="Base image which allows using of source-to-image."	\
    DESCRIPTION="The s2i-core image provides any images layered on top of it \
with all the tools needed to use source-to-image functionality while keeping \
the image size as small as possible."

LABEL summary="$SUMMARY" \
      description="$DESCRIPTION" \
      io.k8s.description="$DESCRIPTION" \
      io.k8s.display-name="s2i core" \
      io.openshift.s2i.scripts-url=image:///usr/libexec/s2i \
      io.s2i.scripts-url=image:///usr/libexec/s2i \
      com.redhat.component="s2i-core-docker" \
      name="hidevopsio/s2i-core-alpine" \
      version="3.6" \
      release="1.0" \
      maintainer="John Deng <john.deng@outlook.com>"

ENV \
    # DEPRECATED: Use above LABEL instead, because this will be removed in future versions.
    STI_SCRIPTS_URL=image:///usr/libexec/s2i \
    # Path to be used in other layers to place s2i scripts into
    STI_SCRIPTS_PATH=/usr/libexec/s2i \
    APP_ROOT=/opt/app-root \
    # The $HOME is not set by default, but some applications needs this variable
    HOME=/opt/app-root/src \
    PATH=/opt/app-root/src/bin:/opt/app-root/bin:$PATH


# When bash is started non-interactively, to run a shell script, for example it
# looks for this variable and source the content of this file. This will enable
# the SCL for all scripts without need to do 'scl enable'.
ENV BASH_ENV=${APP_ROOT}/etc/scl_enable \
    ENV=${APP_ROOT}/etc/scl_enable \
    PROMPT_COMMAND=". ${APP_ROOT}/etc/scl_enable"

# This is the list of basic dependencies that all language container image can
# consume.
# Also setup the 'openshift' user that is used for the build execution and for the
# application runtime execution.
# TODO: Use better UID and GID values
# Network Security Services (NSS) is a set of libraries designed to support cross-platform development of security-enabled client and server applications.

RUN apk update && apk upgrade && \
  INSTALL_PKGS="gettext groff bash" && \
  mkdir -p ${HOME}/.pki/nssdb && \
  chown -R 1001:0 ${HOME}/.pki && \
  apk add $INSTALL_PKGS

# Copy extra files to the image.
COPY ./root/ /

# Directory with the sources is set as the working directory so all STI scripts
# can execute relative to this path.

# Reset permissions of modified directories and add default user
RUN mkdir -p ${HOME} && \
    adduser -u 1001 -S -G root -g 0 -D -h ${HOME} -s /sbin/nologin sti && \
    chown -R 1001:0 ${APP_ROOT}

WORKDIR ${HOME}

ENTRYPOINT ["container-entrypoint"]
CMD ["base-usage"]