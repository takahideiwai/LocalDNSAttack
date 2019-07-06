#Base image Jupiter notebook
FROM jupyter/base-notebook:61d8aaedaeaf


MAINTAINER Takahide Iwai "tiwai@purdue.edu"

# Change the permission to root in order to configure this container
USER root

# allow jovyan to execute certain sudo commands without a password
ADD usersudo /etc/sudoers.d/
RUN chmod 0400 /etc/sudoers.d/usersudo

# install necessary tools
RUN apt-get update 
RUN apt-get install -y bind9 vim net-tools iputils-ping

#Copy DNS config files
COPY named.conf /etc/bind
COPY named.conf.options /etc/bind
COPY named.conf.local /etc/bind
COPY example.com.db /etc/bind
COPY 172.17.0.db /etc/bind

#Bypass authentication
CMD ["start-notebook.sh","--NotebookApp.token="]
