# Taken from https://github.com/Homegear/Homegear-Docker/blob/master/rpi-stable/Dockerfile
ARG BUILD_FROM
ARG BUILD_ARCH

FROM $BUILD_FROM
MAINTAINER Kreativmonkey <kreativmonkey@calyrium.org>


RUN \
    apt-get update && apt-get -y install \
    apt-transport-https \
    wget ca-certificates \
    apt-utils \
    gnupg \
    libzip4 \
    libavahi-client3 \
    libavahi-client-dev \
    insserv
ENV architecture=${BUILD_ARCH}
COPY script/installNightly.sh /installNightly.sh
RUN \
    touch /tmp/HOMEGEAR_STATIC_INSTALLATION; \
    curl https://apt.homegear.eu/Release.key | apt-key add - ; \

    echo 'deb https://apt.homegear.eu/Debian/ buster/' > /etc/apt/sources.list.d/homegear.list; \ 

# Update package information
apt update; \

# Install Homegear with all modules
apt install \
homegear \
homegear-management \
homegear-nodes-core \
homegear-nodes-extra \
homegear-homematicbidcos \
homegear-homematicwired \
homegear-insteon \
homegear-max \
homegear-philipshue \
homegear-sonos \
homegear-kodi \
homegear-ipcam \
homegear-beckhoff \
homegear-knx \
homegear-enocean \
homegear-intertechno \
homegear-nanoleaf \
homegear-ccu \
homegear-mbus \
homegear-influxdb; \    
    
    rm -f /etc/homegear/dh1024.pem; \
    rm -f /etc/homegear/homegear.crt; \
    rm -f /etc/homegear/homegear.key; \
    cp -R /etc/homegear /etc/homegear.config; \
    cp -R /var/lib/homegear /var/lib/homegear.data; \
    apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

COPY script/run.sh /run.sh
RUN chmod +x /run.sh
ENTRYPOINT ["/bin/bash", "-c", "/run.sh"]

EXPOSE 2001 2002 2003
