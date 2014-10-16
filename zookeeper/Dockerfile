FROM ubuntu:trusty

MAINTAINER Tom Cameron tomc603@gmail.com

# Environment Variables
ENV MYID 001

# Install the Java JRE
RUN apt-get update && apt-get install -y default-jre-headless

# Download ZooKeeper
RUN /usr/bin/curl http://www.us.apache.org/dist/zookeeper/current/zookeeper-3.4.6.tar.gz -o /tmp/zookeeper-3.4.6.tar.gz

# Create required directories
RUN mkdir -p /opt && \
    mkdir -p /var/lib/zookeeper/data && \
    mkdir /var/lib/zookeeper/log

# Extract ZooKeeper, delete download
RUN tar -xz -C /opt -f /tmp/zookeeper-3.4.6.tar.gz && \
    rm /tmp/zookeeper-3.4.6.tar.gz

# Create config file
RUN echo "tickTime=2000" > /opt/zookeeper-3.4.6/conf/zoo.cfg
RUN echo "initLimit=5" >> /opt/zookeeper-3.4.6/conf/zoo.cfg
RUN echo "syncLimit=2" >> /opt/zookeeper-3.4.6/conf/zoo.cfg
RUN echo "dataDir=/var/lib/zookeeper/data" >> /opt/zookeeper-3.4.6/conf/zoo.cfg
RUN echo "dataLogDir=/var/lib/zookeeper/log" >> /opt/zookeeper-3.4.6/conf/zoo.cfg
RUN echo "clientPort=2181" >> /opt/zookeeper-3.4.6/conf/zoo.cfg
RUN echo "$MYID" > /opt/zookeeper-3.4.6/conf/myid

EXPOSE 2181 2888 3888

CMD ["/opt/zookeeper-3.4.6/bin/zkServer.sh", "start-foreground"]
