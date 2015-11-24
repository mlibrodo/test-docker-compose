# DOCKER-VERSION 0.11.1
FROM centos:centos6

# Install supervisor
RUN yum install -y python-setuptools && \
	easy_install supervisor && \
	easy_install supervisor-stdout

# Install unzip, wget, tar
RUN yum install -y unzip wget tar

# Install Compilation tool
RUN yum install -y gcc m4 automake libtool && \
    wget ftp://ftp.pbone.net/mirror/ftp5.gwdg.de/pub/opensuse/repositories/home:/monkeyiq:/centos6updates/CentOS_CentOS-6/noarch/autoconf-2.69-12.2.noarch.rpm && \
	yum install -y autoconf-2.69-12.2.noarch.rpm && \
	rm autoconf-2.69-12.2.noarch.rpm

# Install redis
RUN wget http://download.redis.io/releases/redis-2.8.3.tar.gz  && \
    tar xzvf redis-2.8.3.tar.gz && \
    cd redis-2.8.3 && \
    make && \
    make PREFIX=/usr/local/redis/2.8.3 install

EXPOSE 6379 

ADD supervisord.conf /etc/supervisor.conf
RUN mkdir -p /var/log/supervisor
CMD ["/usr/bin/supervisord", "-n", "-c", "/etc/supervisor.conf"]
