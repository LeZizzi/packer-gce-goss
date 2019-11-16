FROM alpine:3.9

ARG PACKER_VERSION=1.4.5
ARG PACKER_VERSION_SHA256SUM=30da8dab9c526a6d15b037e2234f6f12cf3accfad77eb2c130738ec1a54cab6d
ARG PACKER_GOSS_VERSION=v0.3.0

COPY packer_${PACKER_VERSION}_linux_amd64.zip .
RUN echo "${PACKER_VERSION_SHA256SUM}  packer_${PACKER_VERSION}_linux_amd64.zip" > checksum && sha256sum -c checksum

RUN /usr/bin/unzip packer_${PACKER_VERSION}_linux_amd64.zip

RUN mkdir -p ~/.packer.d/plugins
RUN wget https://github.com/YaleUniversity/packer-provisioner-goss/releases/download/${PACKER_GOSS_VERSION}/packer-provisioner-goss-${PACKER_GOSS_VERSION}-linux-amd64 -O ~/.packer.d/plugins/packer-provisioner-goss
RUN chmod +x ~/.packer.d/plugins/packer-provisioner-goss

FROM ubuntu
RUN apt-get -y update && apt-get -y install ca-certificates && rm -rf /var/lib/apt/lists/*
COPY --from=0 packer /usr/bin/packer
ENTRYPOINT ["/usr/bin/packer"]
