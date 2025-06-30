FROM node:8.17.0

ENV BTLEJUICE_ProxyAddress=127.0.0.1
ARG DEBIAN_FRONTEND=noninteractive

# Patch apt sources and install packages

RUN sed -i 's|deb.debian.org|archive.debian.org|g' /etc/apt/sources.list && \
sed -i '/security.debian.org/d' /etc/apt/sources.list && \
sed -i '/stretch-updates/d' /etc/apt/sources.list && \
apt-get update && \
apt-get -qq install -y bluetooth bluez libbluetooth-dev libudev-dev

# Install btlejuice and required components

RUN npm install -g btlejuice --unsafe-perm && \
npm install -g n && \
n 8.9.0 && \
npm install bluetooth-hci-socket --unsafe-perm

EXPOSE 8080

ENTRYPOINT btlejuice -u $BTLEJUICE_ProxyAddress -w
