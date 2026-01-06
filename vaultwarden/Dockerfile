ARG BUILD_FROM=ghcr.io/hassio-addons/debian-base:9.1.0

###############################################################################
# Get prebuild containers from Vaultwarden
###############################################################################
FROM "vaultwarden/server:1.35.2" AS vaultwarden

###############################################################################
# Build the actual add-on.
###############################################################################
# hadolint ignore=DL3006
FROM ${BUILD_FROM}

# Set shell
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

# Get the Bitwarden from official images
COPY --from=vaultwarden /vaultwarden /opt/vaultwarden
COPY --from=vaultwarden /web-vault /opt/web-vault

# add Nginx
# hadolint ignore=DL3009
RUN \
    apt-get update \
    \
    && apt-get install -y --no-install-recommends \
        libmariadb-dev-compat \
        libpq5 \
        nginx \
        sqlite3 \
    && apt-get clean \
    && rm -f -r \
        /etc/nginx \
    \
    && mkdir -p /var/log/nginx \
    && touch /var/log/nginx/error.log

# Copy root filesystem
COPY rootfs /

# Build arguments
ARG BUILD_NAME=Vaultwarden
ARG BUILD_DESCRIPTION="Vaultwarden - password management add-on for Home Assistant"
ARG BUILD_ARCH=aarch64
ARG BUILD_REPOSITORY=mariorasch/ha-add-ons
ARG BUILD_DATE
ARG BUILD_REV=1
ARG BUILD_VERSION=1.0.3

# Labels
LABEL \
    io.hass.name="${BUILD_NAME}" \
    io.hass.description="${BUILD_DESCRIPTION}" \
    io.hass.arch="${BUILD_ARCH}" \
    io.hass.type="addon" \
    io.hass.version="${BUILD_VERSION}" \
    maintainer="Mario Rasch <mario.rasch@web.de>" \
    org.opencontainers.image.title="${BUILD_NAME}" \
    org.opencontainers.image.description="${BUILD_DESCRIPTION}" \
    org.opencontainers.image.vendor="Home Assistant Add-ons by Mario Rasch" \
    org.opencontainers.image.authors="Mario Rasch <mario.rasch@web.de>" \
    org.opencontainers.image.licenses="MIT" \
    org.opencontainers.image.url="https://ghcr.io/mariorasch/ha-add-on-vaultwarden" \
    org.opencontainers.image.source="https://github.com/${BUILD_REPOSITORY}" \
    org.opencontainers.image.documentation="https://github.com/${BUILD_REPOSITORY}/blob/main/vaultwarden/DOCS.md" \
    org.opencontainers.image.created="${BUILD_DATE}" \
    org.opencontainers.image.revision="${BUILD_REV}" \
    org.opencontainers.image.version="${BUILD_VERSION}"
