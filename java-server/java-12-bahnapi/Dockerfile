FROM centos:7
# Prepare PVC moint points
RUN mkdir /projects \
 && chown -R :0 /projects \
 && chmod -R g+rwx /projects \
 && chmod -R o+rx /projects
RUN yum-config-manager --save --setopt=base.skip_if_unavailable=true \
 && yum -y install nano \
 && yum -y install epel-release \
 && yum -y install joe \
 && yum -y install man \
 && yum -y install telnet \
 && yum -y install rsync
RUN yum -y install java-latest-openjdk.x86_64 \
 && yum -y install java-latest-openjdk-javadoc.x86_64 \
 && yum -y install java-latest-openjdk-src.x86_64
RUN yum -y install ant \
 && yum -y install maven \
 && yum -y install bzip2 \
 && yum -y install p7zip \
 && yum -y install wget \
 && yum -y install libtool-ltdl-devel \
 && yum -y install screen.x86_64 \
 && yum -y install libtool-ltdl-devel \
 && yum -y install which \
 && yum -y install net-tools \
 && yum -y install iproute \
 && yum -y install cifs-utils.x86_64 \
 && yum -y install autofs.x86_64 \
 && yum -y upgrade
RUN yum -y install curl-devel expat-devel gettext-devel openssl-devel zlib-devel perl-ExtUtils-MakeMaker
RUN yum -y groupinstall "Development Tools"
RUN echo alias ll='ls -l --color=auto' >> /etc/profile
RUN touch /.bash_history
RUN cp /root/.bash* / \
 && chown -R :0 /.bash* \
 && chmod -R g+rw /.bash* \
 && chmod -R o+r /.bash* \
 && echo PS1=\"\\[\\w\\]\\nuser@\\h:\\\\$ \" >> \.bashrc \
 && echo cd /projects/ >> /.bashrc \
 && echo export no_proxy=$no_proxy,10.104.204.110 >> /.bashrc \
 && echo export NO_PROXY=$no_proxy,10.104.204.110 >> /.bashrc
RUN chown -R :0 /mnt \
 && chmod -R g+rwx /mnt \
 && chmod -R o+rx /mnt
COPY payload/bahnapi.jar /
RUN chown :0 /*.jar
RUN chmod g+rw /*.jar

VOLUME /projects
