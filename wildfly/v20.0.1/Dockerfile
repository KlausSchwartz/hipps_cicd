FROM bitnami/wildfly:20.0.1
USER root

#backup configuration and data
RUN mv -f /opt/bitnami /opt/jboss


RUN cp -rf /opt/jboss/wildfly/standalone /opt/jboss/wildfly/standalone.bak
RUN mkdir -p /opt/jboss/wildfly/modules/com/mysql/main/

#RUN mkdir -p /opt/jboss/wildfly/modules/org/mariadb/jdbc/main
RUN mkdir -p /opt/jboss/wildfly/modules/system/layers/base/org/mariadb/jdbc/main

COPY payload/startup.sh /opt/jboss/wildfly/bin/
COPY payload/mysql/* /opt/jboss/wildfly/modules/com/mysql/main/

# COPY payload/mariadb/* /opt/jboss/wildfly/modules/org/mariadb/jdbc/main/
COPY payload/mariadb/* /opt/jboss/wildfly/modules/system/layers/base/org/mariadb/jdbc/main/


COPY payload/camunda/modules /opt/jboss/wildfly/modules/
COPY payload/camunda/camunda-engine-rest-7.14.0-ee-wildfly.war /opt/jboss/wildfly/standalone/deployments
COPY payload/camunda/camunda-webapp-ee-jboss-7.14.0-ee.war /opt/jboss/wildfly/standalone/deployments



RUN chown -R :0 /opt \
 && chmod -R g+rwx /opt \
 && chmod -R o+rx /opt \
 && chown -R :0 /usr/lib \
 && chmod -R g+rwx /usr/lib \
 && chmod -R o+rx /usr/lib

#RUN yum-config-manager --save --setopt=base.skip_if_unavailable=true --disablerepo=extras

RUN apt-get update
RUN apt-get install -y joe
RUN apt-get install -y telnet
RUN apt-get install -y ant
RUN apt-get install -y maven
RUN apt-get install -y wget
RUN apt-get install -y less
RUN apt-get install -y locales-all
RUN apt-get install -y locales
RUN apt-get upgrade

RUN dpkg-reconfigure locales
RUN locale-gen

#RUN yum -y install nano \
# && yum -y install epel-release \
# && yum -y install joe \
# && yum -y install man \
# && yum -y install telnet \
# && yum -y install rsync \
# && yum -y install ant \
# && yum -y install maven \
# && yum -y install wget \
# && yum -y install libtool-ltdl-devel \
# && yum -y install net-tools \
# && yum -y install iproute \
# && yum -y upgrade
 
#RUN echo alias ll='ls -l --color=auto' >> /etc/profile
RUN echo alias ll="ls -l --color=auto" >> /etc/profile
RUN touch /.bash_history \
 && cp /root/.bash* / \
 && chown -R :0 /.bash* \
 && chmod -R g+rw /.bash* \
 && chmod -R o+r /.bash* \
 && echo PS1=\"\\[\\w\\]\\nuser@\\h:\\\\$ \" >> \.bashrc \
 && echo cd /opt/jboss/wildfly >> /.bashrc

RUN rm -rf /bitnami

VOLUME /opt/jboss/wildfly/standalone/deployments
VOLUME /opt/jboss/wildfly/standalone/data
VOLUME /opt/jboss/wildfly/standalone/configuration
VOLUME /opt/jboss/wildfly/standalone/log

ENV JBOSS_HOME /opt/jboss/wildfly
ENTRYPOINT /opt/jboss/wildfly/bin/startup.sh
