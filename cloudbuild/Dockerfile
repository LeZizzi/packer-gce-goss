FROM alpine:3.9

ARG PACKER_VERSION=1.5.1
ARG PACKER_VERSION_SHA256SUM=3305ede8886bc3fd83ec0640fb87418cc2a702b2cb1567b48c8cb9315e80047d
ARG PACKER_GOSS_VERSION=v0.3.0

COPY packer_${PACKER_VERSION}_linux_amd64.zip .
COPY packer-provisioner-goss-${PACKER_GOSS_VERSION}-linux-amd64 .
RUN echo "${PACKER_VERSION_SHA256SUM}  packer_${PACKER_VERSION}_linux_amd64.zip" > checksum && sha256sum -c checksum

RUN /usr/bin/unzip packer_${PACKER_VERSION}_linux_amd64.zip
RUN chmod +x packer-provisioner-goss-${PACKER_GOSS_VERSION}-linux-amd64 && mv packer-provisioner-goss-${PACKER_GOSS_VERSION}-linux-amd64 packer-provisioner-goss

FROM ubuntu
RUN apt-get -y update && apt-get -y install ca-certificates && rm -rf /var/lib/apt/lists/*
COPY --from=0 packer /usr/bin/packer
COPY --from=0 packer-provisioner-goss  /usr/bin/packer-provisioner-goss
ENTRYPOINT ["/usr/bin/packer"]
