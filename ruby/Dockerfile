FROM centos

MAINTAINER kaihara

# set password
RUN echo 'root:root' | chpasswd

RUN yum -y update

# configure for ssh
RUN yum -y install openssh-server
RUN sed -ri 's/UsePAM yes/UsePAM no/' /etc/ssh/sshd_config
RUN /etc/init.d/sshd start ; /etc/init.d/sshd stop

RUN yum -y groupinstall "Base"
RUN yum -y groupinstall "Development Tools"
RUN yum -y install --enablerepo=centosplus openssl-devel

ENV HOME /root
ENV PATH $HOME/.rbenv/bin:$HOME/.rbenv/shims:$PATH

# Install ruby
RUN git clone git://github.com/sstephenson/rbenv.git $HOME/.rbenv
RUN git clone git://github.com/sstephenson/ruby-build.git $HOME/.rbenv/plugins/ruby-build
RUN rbenv install 2.0.0-p451
RUN rbenv global 2.0.0-p451
RUN rbenv rehash
RUN gem install bundler
RUN rbenv rehash

RUN echo 'export PATH=$HOME/.rbenv/bin:$HOME/.rbenv/shims:$PATH' >> $HOME/.bashrc
RUN echo 'eval "$(rbenv init -)"' >> $HOME/.bashrc

EXPOSE 22 4567

CMD /usr/sbin/sshd -D
