FROM debian:stretch

ARG hostname
# "" == latest
ARG salt_ver=""

COPY minion/entrypoint_minion_run.sh /opt/
COPY minion/minion.conf /etc/salt/minion.d/minion.conf
COPY minion/supervisord_minion.conf /etc/supervisor/conf.d/supervisord.conf

RUN echo $(grep $(hostname) /etc/hosts | cut -f1) $hostname >> /etc/hosts && \
    apt-get update && \
    apt-get install -y curl supervisor procps && \
    curl -o /tmp/bootstrap-salt.sh -L https://bootstrap.saltstack.com && \
    sh /tmp/bootstrap-salt.sh -n -X stable $salt_ver

ENTRYPOINT ["/opt/entrypoint_minion_run.sh"]
