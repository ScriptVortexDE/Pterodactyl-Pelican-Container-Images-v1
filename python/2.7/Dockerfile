FROM        python:2.7-slim

LABEL       author="Auroa Online" maintainer="hello@auroa.cloud"
LABEL       org.opencontainers.image.source="https://github.com/ScriptVortexDE/Pterodactyl-Pelican-Container-Images-v1"
LABEL       org.opencontainers.image.licenses="MIT"

# Debian buster is EOL and only available on archive.debian.org
RUN         printf 'deb http://archive.debian.org/debian buster main\ndeb http://archive.debian.org/debian-security buster/updates main\n' > /etc/apt/sources.list \
            && rm -f /etc/apt/sources.list.d/*.list /etc/apt/sources.list.d/*.sources \
            && printf 'Acquire::Check-Valid-Until "false";\n' > /etc/apt/apt.conf.d/99archive

RUN         apt-get update \
            && apt-get -y install --no-install-recommends git gcc g++ ca-certificates dnsutils curl iproute2 ffmpeg procps locales \
            && apt-get clean \
            && rm -rf /var/lib/apt/lists/* \
            && useradd -m -d /home/container container \
            && locale-gen en_US.UTF-8

ENV         LC_ALL=en_US.UTF-8
ENV         LANG=en_US.UTF-8
ENV         LANGUAGE=en_US.UTF-8

USER        container
ENV         USER=container HOME=/home/container
WORKDIR     /home/container

COPY        ./entrypoint.sh /entrypoint.sh
CMD         [ "/bin/bash", "/entrypoint.sh" ]
