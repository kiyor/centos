FROM centos:centos6
MAINTAINER Kiyor Cai <cai@kiyor.com>

RUN yum -y install openssh-server epel-release && \
    yum -y install pwgen && \
    yum -y install supervisor && \
    rm -f /etc/ssh/ssh_host_dsa_key /etc/ssh/ssh_host_rsa_key && \
    ssh-keygen -q -N "" -t dsa -f /etc/ssh/ssh_host_dsa_key && \
    ssh-keygen -q -N "" -t rsa -f /etc/ssh/ssh_host_rsa_key && \
    sed -i "s/#UsePrivilegeSeparation.*/UsePrivilegeSeparation no/g" /etc/ssh/sshd_config && \
    sed -i "s/UsePAM.*/UsePAM no/g" /etc/ssh/sshd_config

ADD supervisord.conf /etc/supervisord.conf
ADD set_root_pw.sh /root/set_root_pw.sh
ADD ssh.sh /root/ssh.sh
RUN chmod +x /root/*.sh

ENV KEY **None**

EXPOSE 22
CMD ["/usr/bin/supervisord"]
