FROM ubuntu
ADD https://apt.puppetlabs.com/puppetlabs-release-trusty.deb /tmp/
ADD http://nightlies.puppetlabs.com/puppetserver-latest/repo_configs/deb/pl-puppetserver-latest-trusty.list \
    /etc/apt/sources.list.d/
ADD http://nightlies.puppetlabs.com/puppet-agent-latest/repo_configs/deb/pl-puppet-agent-latest-trusty.list \
    /etc/apt/sources.list.d/
RUN dpkg --install /tmp/puppetlabs-release-trusty.deb && \
    mkdir --parents /opt/puppetlabs/server/apps/puppetserver && \
    ln -s /opt/puppetlabs/server/apps/puppetserver /usr/share/puppetserver && \
    apt-get update && \
    apt-get install -y --force-yes puppetserver && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* && \
    sed --in-place 's/JAVA_ARGS="-Xms2g -Xmx2g/JAVA_ARGS="-Xms512m -Xmx512m/' \
        /etc/default/puppetserver

EXPOSE 8140

ENTRYPOINT [ "/usr/bin/puppetserver", "foreground" ]
