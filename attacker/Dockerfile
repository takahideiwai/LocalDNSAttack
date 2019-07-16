FROM dorowu/ubuntu-desktop-lxde-vnc:bionic


MAINTAINER Takahide Iwai "tiwai@purdue.edu"

# Check if it runs without libpcap-dev libnet1-dev tcl libcap2-bin

#add necessary tools

RUN add-apt-repository ppa:wireshark-dev/stable
RUN apt-get update && apt-get -y install net-tools vim iputils-ping dnsutils \
apache2 netwox openssh-server wireshark nmap  \
dsniff gedit scapy netwag


#create a non-root user
RUN useradd -d /home/attacker -m -s /bin/bash attacker

RUN echo 'attacker:attacker' | chpasswd

ENV USER=attacker \
    PASSWORD=attacker 

RUN usermod -aG sudo attacker

#Set necessary configurations for wireshark

RUN groupadd wireshark
RUN usermod -a -G wireshark attacker
RUN chgrp wireshark /usr/bin/dumpcap
RUN chmod 750 /usr/bin/dumpcap
RUN setcap cap_net_raw,cap_net_admin=eip /usr/bin/dumpcap
RUN getcap /usr/bin/dumpcap


# Copy necessary configuration files
COPY ports.conf /etc/apache2/
COPY 000-default.conf /etc/apache2/sites-available
COPY attack.py /home/attacker

#Allow user to run certain commands without a password
ADD attackersudo /etc/sudoers.d/
RUN chmod 0400 /etc/sudoers.d/attackersudo


