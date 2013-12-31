# This file describes how to build Plone into a runnable linux container with all dependencies installed
# To build:
# 1) Install docker (http://docker.io)
# 2) Run:
# docker run -d <imageid>
#
# VERSION                0.1
# DOCKER-VERSION        0.7.2

from        ubuntu:12.04
MAINTAINER Gauthier C.
run        echo "deb http://archive.ubuntu.com/ubuntu precise main universe" > /etc/apt/sources.list
run        apt-get update
run        apt-get upgrade -y
run        apt-get -y install wget git build gcc patch python-dev make libxml2 python-libxml2 python-libxslt1 libxslt1-dev python-ldap libldap2-dev libsasl2-dev libpcre3-dev
run        wget -O - https://launchpad.net/plone/4.3/4.3.2/+download/Plone-4.3.2-UnifiedInstaller.tgz | tar -C /tmp/ -zxv
run        mkdir -p /usr/local/Zeo/zeocluster
run        /tmp/Plone-4.3.2-UnifiedInstaller/install.sh zeo --target=/usr/local/Zeo/
run        git clone https://github.com/gauthierc/confPloneZeo.git /usr/local/Zeo/zeocluster
run        /usr/local/Zeo/zeocluster/bin/buildout -c deployement.cfg
expose     5501
cmd        ["/usr/local/Zeo/zeocluster/bin/supervisord", "-n"]