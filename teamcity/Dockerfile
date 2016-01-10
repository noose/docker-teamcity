FROM phusion/baseimage:0.9.18
MAINTAINER Pawel Kobylak <noose@noose.pl>
RUN apt-get update
RUN apt-get install -y --no-install-recommends openjdk-7-jdk git
RUN apt-get install -y --no-install-recommends wget

ENV TEAMCITY_VERSION 9.1.5
RUN mkdir -p /var/lib/teamcity \
    && groupadd -g 999 teamcity \
    && useradd -u 999 -g teamcity -d /var/lib/teamcity teamcity \
    && chown -R teamcity:teamcity /var/lib/teamcity \
    && wget -O- http://download.jetbrains.com/teamcity/TeamCity-$TEAMCITY_VERSION.tar.gz | tar xz -C /opt \
    && chown -R teamcity:teamcity /opt/TeamCity

RUN apt-get clean
RUN rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*


ADD .BuildServer /var/lib/teamcity/.BuildServer

RUN chown -R teamcity:teamcity /var/lib/teamcity
WORKDIR /var/lib/teamcity/
USER teamcity
EXPOSE 8111
CMD ["/opt/TeamCity/bin/teamcity-server.sh", "run"]
