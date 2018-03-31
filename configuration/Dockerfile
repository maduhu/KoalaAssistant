FROM ubuntu:17.10

RUN useradd kylo
VOLUME /tmp/config

ADD kylo-0.9.0.1.deb .
RUN dpkg -i kylo-0.9.0.1.deb

RUN /opt/kylo/setup/generate-offline-install.sh && \
    tar -xvf /opt/kylo/setup/kylo-install.tar

ENTRYPOINT ["ls", "-l", "/opt/kylo/setup"]
