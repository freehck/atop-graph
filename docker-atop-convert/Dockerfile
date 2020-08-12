FROM ubuntu:18.04

ENV DEBIAN_FRONTEND  noninteractive
ENV INFLUXDB_VERSION 0.13.0

RUN \
    apt-get -y update && apt-get -y upgrade ; \
    apt-get -y install wget libfontconfig ;\
    wget -q https://dl.influxdata.com/influxdb/releases/influxdb_${INFLUXDB_VERSION}_amd64.deb && \
    dpkg -i influxdb_${INFLUXDB_VERSION}_amd64.deb && rm influxdb_${INFLUXDB_VERSION}_amd64.deb

#RUN \
#    set -x -e; \
#    apt-get install -y build-essential zlib1g-dev make libncurses-dev ;\
#    wget http://www.atoptool.nl/download/atop-2.3.0.tar.gz  && tar -xvzf atop-2.3.0.tar.gz  && rm atop-2.3.0.tar.gz  ;\
#    D=$(pwd); ls -la / /root ; \
#    rm -f /etc/atop/atop.daily /etc/rc.d/init.d/atop /etc/cron.d/atop ; \
#    ls -la /usr/bin/a* /usr/sbin/a* ;\
#    apt-get remove -y build-essential make; apt-get autoremove -y

RUN apt-get install -y atop

RUN rm -f /etc/systemd/system/influxd.service /etc/systemd/system/multi-user.target.wants/influxdb.service

ADD     parse.awk       /
ADD     convert.sh      /

CMD     ["/convert.sh"]
