FROM debian:buster-slim

LABEL description="SinusBot - Discord only image"
LABEL version="1.0.0-beta.10-202ee4d"

# Install dependencies and clean up afterwards
RUN apt-get update && \
    apt-get install -y --no-install-recommends ca-certificates bzip2 unzip curl python procps libpci3 libxslt1.1 libxkbcommon0 && \
    rm -rf /tmp/* /var/tmp/* /var/lib/apt/lists/*

WORKDIR /opt/sinusbot

ADD install.sh .
RUN chmod 755 install.sh

# Download/Install SinusBot
RUN bash install.sh sinusbot

# Download/Install youtube-dl
RUN bash install.sh youtube-dl

# Download/Install Text-to-Speech
RUN bash install.sh text-to-speech

ADD entrypoint.sh .
RUN chmod 755 entrypoint.sh

EXPOSE 8087

VOLUME ["/opt/sinusbot/data", "/opt/sinusbot/scripts"]

ENTRYPOINT ["/opt/sinusbot/entrypoint.sh"]

HEALTHCHECK --interval=1m --timeout=10s \
  CMD curl --no-keepalive -f http://localhost:8087/api/v1/botId || exit 1
