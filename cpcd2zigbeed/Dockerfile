ARG BUILD_BASE=ghcr.io/jnilo1/cpcd-zigbeed
ARG BUILD_FROM=ghcr.io/hassio-addons/ubuntu-base:stable

FROM ${BUILD_BASE} AS base
FROM ${BUILD_FROM}

ARG BUILD_ARCH
ARG BUILD_VERSION
ARG BUILD_DESCRIPTION
ARG BUILD_NAME
ARG BUILD_REF
ARG BUILD_REPOSITORY
ARG UPSTREAM_REPOSITORY
ARG UPSTREAM_REVISION
ARG UPSTREAM_IMAGE
ARG UPSTREAM_VERSION


RUN apt-get -y update && apt-get install -y --no-install-recommends \
    netcat-openbsd \
    gettext-base \
    procps \
    && rm -rf /var/lib/apt/lists/*

# app-ubuntu-base already provides Ubuntu LTS, s6, jq, curl, Bashio and tempio.
# Only the selected cpcd/zigbeed runtime pieces are copied from the upstream image.
COPY rootfs /

COPY --from=base /usr/local/bin/cpcd /usr/local/bin/zigbeed /usr/local/bin/
COPY --from=base /usr/local/lib/* /usr/local/lib/
COPY --from=base /usr/share/doc/zigbeed/THIRD_PARTY_NOTICES /usr/share/doc/zigbeed/

RUN chmod 0755 \
      /usr/local/bin/cpcd \
      /usr/local/bin/zigbeed \
      /etc/cont-init.d/10-cpcd2zigbeed \
      /etc/services.d/cpcd/run \
      /etc/services.d/cpcd/finish \
      /etc/services.d/zigbeed/run \
      /etc/services.d/zigbeed/finish \
    && ldconfig

LABEL \
    io.hass.arch="${BUILD_ARCH}" \
    io.hass.type="app" \
    io.hass.version="${BUILD_VERSION}" \
    org.opencontainers.image.title="${BUILD_NAME}" \
    org.opencontainers.image.description="${BUILD_DESCRIPTION}" \
    org.opencontainers.image.source="https://github.com/${BUILD_REPOSITORY}" \
    org.opencontainers.image.revision="${UPSTREAM_REVISION}" \
    org.opencontainers.image.version="${BUILD_VERSION}" \
    io.hassio.upstream.repository="${UPSTREAM_REPOSITORY}" \
    io.hassio.upstream.revision="${UPSTREAM_REVISION}" \
    io.hassio.upstream.image="${UPSTREAM_IMAGE}" \
    io.hassio.upstream.version="${UPSTREAM_VERSION}" \
    maintainer="Damien Gaignon <damien.gaignon@gmail.com>" \
    org.opencontainers.image.authors="Damien Gaignon <damien.gaignon@gmail.com>" \
    org.opencontainers.image.url="https://github.com/${BUILD_REPOSITORY}"

