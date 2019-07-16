FROM dorowu/ubuntu-desktop-lxde-vnc:bionic

MAINTAINER Takahide Iwai "tiwai@purdue.edu"

#add John the ripper and gedit 
RUN apt-get update && apt-get -y install net-tools vim iputils-ping dnsutils openssh-server

#create a non-root user
RUN useradd -d /home/victim -m -s /bin/bash victim

RUN echo 'victim:victim' | chpasswd

ENV USER=victim \
    PASSWORD=victim 
RUN usermod -aG sudo victim

#Allow user to run certain commands without a password
ADD victimsudo /etc/sudoers.d/
RUN chmod 0400 /etc/sudoers.d/victimsudo

