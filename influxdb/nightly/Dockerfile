FROM buildpack-deps:jessie-curl
MAINTAINER Arkka Dhiratara <arkka.d@gmail.com>

RUN gpg \
    --keyserver hkp://ha.pool.sks-keyservers.net \
    --recv-keys 05CE15085FC09D18E99EFB22684A14CF2582E0C5

RUN wget -q https://dl.influxdata.com/influxdb/nightlies/influxdb_nightly_amd64.deb.asc && \
    wget -q https://dl.influxdata.com/influxdb/nightlies/influxdb_nightly_amd64.deb && \
    gpg --batch --verify influxdb_nightly_amd64.deb.asc influxdb_nightly_amd64.deb && \
    dpkg -i influxdb_nightly_amd64.deb && \
    rm -f influxdb_nightly_amd64.deb*
COPY types.db /usr/share/collectd/types.db
COPY influxdb.conf /etc/influxdb/influxdb.conf

EXPOSE 8083 8086 8096/udp 2003

VOLUME /var/lib/influxdb

COPY entrypoint.sh /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]
CMD ["influxd"]
