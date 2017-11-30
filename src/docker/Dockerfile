FROM centos:latest

ENV JAVA_VERSION 8u151
ENV BUILD_VERSION b13
# Upgrading system
RUN yum -y upgrade
RUN yum -y install wget unzip curl
# Downloading & Config Java 8
RUN wget --no-cookies --no-check-certificate --header "Cookie: gpw_e24=http%3A%2F%2Fwww.oracle.com%2F; oraclelicense=accept-securebackup-cookie" "http://download.oracle.com/otn-pub/java/jdk/8u151-b12/e758a0de34e24606bca991d704f6dcbf/jdk-8u151-linux-x64.rpm" -O /tmp/jdk-8-linux-x64.rpm
RUN yum -y install /tmp/jdk-8-linux-x64.rpm
RUN alternatives --install /usr/bin/jar jar /usr/java/latest/bin/java 200000
RUN alternatives --install /usr/bin/javaws javaws /usr/java/latest/bin/javaws 200000
RUN alternatives --install /usr/bin/javac javac /usr/java/latest/bin/javac 200000

ENV JAVA_OPTS=
WORKDIR /data
VOLUME ["/data/ignite-2.3.0/work"]
RUN yum update && yum install -y unzip curl
RUN wget https://s3.us-east-2.amazonaws.com/cecl-ignite/ignite-2.3.0.zip
RUN unzip ignite-2.3.0.zip
RUN chmod +x /data/ignite-2.3.0/bin/ignite.sh
ENTRYPOINT ["/data/ignite-2.3.0/bin/ignite.sh","/data/ignite-2.3.0/config/loss-amount-config.xml", "-v"]

EXPOSE 11211 47100 47500 49112