FROM debian:stretch

ARG hostname
ARG saltenv
ARG pillarenv
# "" == latest
ARG salt_ver=""

COPY no_daemon_env /etc/default/salt-master
COPY master/master.conf /etc/salt/master.d/master.conf
COPY master/reactor_master.conf /etc/salt/master.d/reactor.conf
COPY master/supervisord_master.conf /etc/supervisor/conf.d/supervisord.conf
COPY master/pillar /srv/pillar
COPY master/salt /srv/salt
COPY master/reactor /srv/reactor

RUN echo $(grep $(hostname) /etc/hosts | cut -f1) $hostname >> /etc/hosts && \
    apt-get update && \
    apt-get install -y curl supervisor procps && \
    curl -o /tmp/bootstrap-salt.sh -L https://bootstrap.saltstack.com && \
    sh /tmp/bootstrap-salt.sh -n -M -N -X stable $salt_ver && \
# workaround for (needed only when installed via Dockerfile)
# https://github.com/saltstack/salt/issues/37056
    rm -rf /var/run/salt/master/master_event_pub.ipc && \
    rm -rf /var/run/salt/master/master_event_pull.ipc    
    
EXPOSE 4505:4505 4506:4506

ENV SALTENV=$saltenv
ENV PILLARENV=$pillarenv
ENV LOG_LEVEL=$log_level

ENTRYPOINT [ "/usr/bin/supervisord" ]
