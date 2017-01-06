FROM openjdk:8

MAINTAINER Hearst Automation Team "atat@hearst.com"

ENV JENKINS_HOME /var/lib/jenkins

RUN apt-get update &&\
    apt-get install -y openssh-server \
    git \
    sudo \
    bash &&\
    apt-get clean -y && rm -rf /var/lib/apt/lists/* &&\
    sed -i 's|session    required     pam_loginuid.so|session    optional     pam_loginuid.so|g' /etc/pam.d/sshd &&\
    mkdir -p /var/run/sshd &&\
    useradd -m -d $JENKINS_HOME -s /bin/bash -U jenkins && \
    echo "jenkins:jenkins" | chpasswd &&\
    echo "%jenkins ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers

USER jenkins

VOLUME /var/lib/jenkins

EXPOSE 22

WORKDIR /var/lib/jenkins

RUN sudo /usr/bin/ssh-keygen -A

CMD ["sudo", "/usr/sbin/sshd", "-D"]
