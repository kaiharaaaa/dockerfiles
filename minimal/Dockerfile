FROM centos

MAINTAINER kaihara

# set password
RUN echo 'root:root' | chpasswd

RUN yum -y update

# configure for ssh
RUN yum -y install openssh-server
RUN sed -ri 's/UsePAM yes/UsePAM no/' /etc/ssh/sshd_config
RUN /etc/init.d/sshd start ; /etc/init.d/sshd stop

EXPOSE 22

CMD /usr/sbin/sshd -D
