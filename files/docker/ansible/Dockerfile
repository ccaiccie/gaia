FROM centos/python-36-centos7:latest

### -------------------------------------------------
### Metadata information
### -------------------------------------------------
LABEL name="nibelheim"
LABEL maintainer="packetferret@gmail.com"
LABEL description="ansible juniper container"
LABEL license="GPLv2"
LABEL url="https://github.com/packetferret/nibelheim"
LABEL build-date="20191031"

### -------------------------------------------------
### Install system Package
### -------------------------------------------------
USER root
RUN yum -y update 
RUN yum -y install vim nmap wget telnet zsh
RUN yum clean all
RUN wget https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - | zsh || true
RUN rm -rf /tmp/* /var/tmp/*

### -------------------------------------------------
### Change directory to /home/tmp
### -------------------------------------------------
WORKDIR /home/tmp/files

### -------------------------------------------------
### Add and install python packages
### -------------------------------------------------
ADD config/requirements.txt requirements.txt
RUN pip install -r requirements.txt
RUN pip install --upgrade pip

### -------------------------------------------------
### Install Ansible Galaxy roles
### -------------------------------------------------
RUN ansible-galaxy install juniper.junos

### -------------------------------------------------
### Copy local files to container
### -------------------------------------------------
COPY config/jsnapy.cfg /etc/jsnapy/jsnapy.cfg
COPY config/.zshrc /opt/app-root/src/.zshrc
COPY config/bullet-train_custom.zsh-theme /opt/app-root/src/.oh-my-zsh/themes/bullet-train_custom.zsh-theme

### -------------------------------------------------
### Change directory to /opt/app-root/src/ansible
### -------------------------------------------------
WORKDIR /opt/app-root/src/ansible

### -------------------------------------------------
### Environmentals
### -------------------------------------------------
ENV HAPPY True
ENV SHELL /usr/bin/zsh
ENV ANSIBLE_CONFIG /opt/app-root/src/ansible/ansible.cfg
