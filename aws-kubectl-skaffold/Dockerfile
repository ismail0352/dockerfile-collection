# FROM bitnami/kubectl:1.20.9 as kubectl

FROM ubuntu:22.04 as binary

RUN apt-get update \
  && apt-get install -y curl unzip

# # AWSCLI
# RUN curl https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip -o awscliv2.zip \
#   && unzip awscliv2.zip \
#   && ./aws/install

# kubectl
RUN curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl" && \
    chmod +x kubectl && \
    mv kubectl /usr/local/bin

# Skaffold
RUN curl -Lo skaffold https://storage.googleapis.com/skaffold/releases/latest/skaffold-linux-amd64 && \
    install skaffold /usr/local/bin/

FROM alpine:latest

# COPY --from=binary /usr/local/bin/aws /usr/local/bin/aws
COPY --from=binary /usr/local/bin/kubectl /usr/local/bin/kubectl
COPY --from=binary /usr/local/bin/skaffold /usr/local/bin/skaffold

RUN apk add --no-cache aws-cli bash jq
