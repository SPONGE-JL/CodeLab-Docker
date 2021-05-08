FROM centos:7

USER root

# Character Set
RUN  yum clean all \
  && yum repolist \
  && yum -y update \
  && sed -i "s/en_US/all/" /etc/yum.conf  \
  && yum -y reinstall glibc-common
  
# OS Default Packages
RUN  yum -y install tar unzip vi vim telnet net-tools curl openssl \
  && yum -y install apr apr-util apr-devel apr-util-devel \
  && yum -y install elinks locate python-setuptools \
  && yum clean all

ENV LANG=ko_KR.utf8 TZ=Asia/Seoul

COPY . .

RUN sed -i "s/@_WHERE_@/CentOS 7 Container/g" local-to-container.txt

CMD ["/bin/bash"]
