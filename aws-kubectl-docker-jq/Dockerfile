FROM ubuntu:22.04 as binary

RUN apt-get update \
  && apt-get install -y curl unzip

# kubectl
RUN curl -LO https://dl.k8s.io/release/v1.29.4/bin/linux/amd64/kubectl && \
    chmod +x kubectl && \
    mv kubectl /usr/local/bin


FROM alpine:latest

COPY --from=binary /usr/local/bin/kubectl /usr/local/bin/kubectl

RUN apk add --no-cache coreutils aws-cli docker-cli bash jq uuidgen yq git gettext curl
