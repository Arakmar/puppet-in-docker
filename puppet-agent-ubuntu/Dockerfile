FROM jrei/systemd-ubuntu
MAINTAINER Gareth Rushgrove "gareth@puppet.com"

ENV PUPPET_AGENT_VERSION="1.9.3" UBUNTU_CODENAME="xenial"

LABEL org.label-schema.vendor="Puppet" \
      org.label-schema.url="https://github.com/puppetlabs/puppet-in-docker" \
      org.label-schema.name="Puppet Agent (Ubuntu)" \
      org.label-schema.license="Apache-2.0" \
      org.label-schema.version=$PUPPET_AGENT_VERSION \
      org.label-schema.vcs-url="https://github.com/puppetlabs/puppet-in-docker" \
      org.label-schema.vcs-ref="a2b1fbbc73177ddc3def23d167f9beb9c3ef9f6c" \
      org.label-schema.build-date="2017-02-21T17:25:14Z" \
      org.label-schema.schema-version="1.0" \
      com.puppet.dockerfile="/Dockerfile"

RUN apt-get update && \
    apt-get install --no-install-recommends -y wget ca-certificates lsb-release cron && \
    wget https://apt.puppetlabs.com/puppetlabs-release-pc1-"$UBUNTU_CODENAME".deb && \
    dpkg -i puppetlabs-release-pc1-"$UBUNTU_CODENAME".deb && \
    rm puppetlabs-release-pc1-"$UBUNTU_CODENAME".deb && \
    apt-get update && \
    apt-get install --no-install-recommends -y puppet-agent="$PUPPET_AGENT_VERSION"-1"$UBUNTU_CODENAME" && \
    apt-get remove --purge -y wget && \
    apt-get autoremove -y && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
    /opt/puppetlabs/puppet/bin/puppet config set autosign true --section master && \
    /opt/puppetlabs/puppet/bin/puppet config set allow_duplicate_certs true --section master && \
    rm /etc/systemd/system/multi-user.target.wants/mcollective.service && \
    rm /etc/systemd/system/multi-user.target.wants/puppet.service;
    
ENV PATH=/opt/puppetlabs/server/bin:/opt/puppetlabs/puppet/bin:/opt/puppetlabs/bin:$PATH

CMD ["/usr/sbin/init"]

COPY Dockerfile /
