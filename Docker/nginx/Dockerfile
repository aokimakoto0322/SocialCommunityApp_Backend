 FROM ubuntu:18.04
 RUN apt update
 RUN apt install -y openssh-server
 RUN mkdir /var/run/sshd
 RUN echo 'root:root' | chpasswd
 RUN sed -ri 's/^#?PermitRootLogin\s+.*/PermitRootLogin yes/' /etc/ssh/sshd_config
 
 # SSH login fix. Otherwise user is kicked off after login
 RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd

 # nginxの環境構築
 RUN apt-get update
 RUN apt-get install -y nginx
 ENTRYPOINT ["nginx", "-g", "daemon off;"]
 
 ENV NOTVISIBLE "in users profile"
 RUN echo "export VISIBLE=now" >> /etc/profile
 ENTRYPOINT [ "/usr/sbin/sshd", "-D" ]