FROM node:8.17.0

ARG DEBIAN_FRONTEND=noninteractive

# Use archived Debian Stretch sources

RUN echo "deb http://archive.debian.org/debian stretch main" > /etc/apt/sources.list && \
echo "deb http://archive.debian.org/debian-security stretch/updates main" >> /etc/apt/sources.list && \
echo 'Acquire::Check-Valid-Until "false";' > /etc/apt/apt.conf.d/99no-check-valid-until && \
apt-get update

# Install required packages

RUN apt-get install -y --no-install-recommends \
bluetooth \
bluez \
libbluetooth-dev \
libudev-dev \
python \
build-essential && \
rm -rf /var/lib/apt/lists/\*

# Install BTLEjuice globally

RUN npm install -g btlejuice --unsafe-perm

# Expose the default BTLEjuice proxy port

EXPOSE 8000

# Start the proxy using hci0 interface (hardcoded)

ENTRYPOINT \["btlejuice-proxy", "--iface", "hci0"\]
