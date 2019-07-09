FROM dorowu/ubuntu-desktop-lxde-vnc:bionic

MAINTAINER Takahide Iwai "tiwai@purdue.edu"

#add necessary tools
RUN apt-get update && apt-get -y install net-tools vim iputils-ping dnsutils apache2

#create a non-root user
RUN useradd -d /home/attacker -m -s /bin/bash attacker

RUN echo 'attacker:attacker' | chpasswd

ENV USER=attacker \
    PASSWORD=attacker 

# Copy necessary configuration files
COPY ports.conf /etc/apache2/
COPY 000-default.conf /etc/apache2/sites-available

#Allow user to run certain commands without a password
ADD attackersudo /etc/sudoers.d/
RUN chmod 0400 /etc/sudoers.d/attackersudo

