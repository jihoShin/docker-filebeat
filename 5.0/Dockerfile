FROM debian:jessie

MAINTAINER Andrea Usuelli <andrea.usuelli@prima.it>

ENV FILEBEAT_VERSION=5.0.1 \
    FILEBEAT_SHA1=b8139a51834f6c0ff90a7de1159c0b2162b86e7e

RUN set -x && \
  apt-get update && \
  apt-get install -y wget && \
  wget https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-${FILEBEAT_VERSION}-linux-x86_64.tar.gz -O /opt/filebeat.tar.gz && \
  cd /opt && \
  echo "${FILEBEAT_SHA1}  filebeat.tar.gz" | sha1sum -c - && \
  tar xzvf filebeat.tar.gz && \
  cd filebeat-* && \
  cp filebeat /bin && \
  cd /opt && \
  rm -rf filebeat* && \
  apt-get purge -y wget && \
  apt-get autoremove -y && \
  apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

COPY docker-entrypoint.sh /

COPY config/filebeat.yml /filebeat.yml

ENTRYPOINT ["/docker-entrypoint.sh"]
CMD [ "filebeat", "-e" ]
