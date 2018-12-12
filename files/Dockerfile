FROM ansible/centos7-ansible
USER root
ADD RPMS/ /tmp/
RUN yum clean all && yum localinstall /tmp/ansible-tower-venv-ansible-3.3.0-1.el7.x86_64.rpm -y && yum localinstall /tmp/ansible-tower-isolated-3.3.0-1.el7.x86_64.rpm -y && yum install openssh-server -y && yum update -y
RUN mkdir -p /var/lib/awx/.ssh/ && chown -R awx:awx /var/lib/awx
RUN ssh-keygen -t rsa -f /etc/ssh/ssh_host_rsa_key -N ''
RUN ssh-keygen -t dsa -f /etc/ssh/ssh_host_dsa_key -N ''
ADD FILES/id_rsa.pub /var/lib/awx/.ssh/authorized_keys
RUN sed -i 's/#PermitRootLogin yes/PermitRootLogin yes/g' /etc/ssh/sshd_config
EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]
