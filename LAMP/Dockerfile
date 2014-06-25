FROM centos

MAINTAINER kaihara

# set password
RUN echo 'root:root' | chpasswd

RUN yum -y update

# configure for ssh
RUN yum -y install openssh-server
RUN sed -ri 's/UsePAM yes/UsePAM no/' /etc/ssh/sshd_config
RUN /etc/init.d/sshd start ; /etc/init.d/sshd stop

# LAMP
RUN yum -y groupinstall "Base"
RUN yum -y groupinstall "Development Tools"
RUN yum -y install httpd-devel mysql-server php php-mbstring php-mysql

# Supervisor
RUN wget http://ftp-srv2.kddilabs.jp/Linux/distributions/fedora/epel/6/x86_64/epel-release-6-8.noarch.rpm
RUN rpm -ivh epel-release-6-8.noarch.rpm
RUN yum --enablerepo=epel -y install supervisor

ADD supervisor/supervisord.conf /etc/supervisord.conf

EXPOSE 22 80 3306

ENTRYPOINT /usr/bin/supervisord -n
