FROM ubuntu:16.04

RUN apt-get update && \
    apt-get install -y openssh-server && \
    apt-get install -y python && \
    apt-get install cron && \
    apt-get install sshpass && \
    apt install -y ucommon-utils
    
RUN mkdir /var/run/sshd
RUN echo 'root:securepasswd' | chpasswd
RUN sed -i 's/PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config

# SSH login fix. Otherwise user is kicked off after login
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd

ENV NOTVISIBLE "in users profile"
RUN echo "export VISIBLE=now" >> /etc/profile

RUN mkdir -p /backup/mysql

EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]