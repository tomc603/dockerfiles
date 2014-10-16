FROM ubuntu:trusty

MAINTAINER Tom Cameron <tomc603@gmail.com>

# Environment Variables
ENV ZK_VERSION 3.4.6
ENV MYID 001

# Install the Java JRE
RUN apt-get update && apt-get install -y curl default-jre-headless

# Download ZooKeeper
RUN /usr/bin/curl http://www.us.apache.org/dist/zookeeper/current/zookeeper-$ZK_VERSION.tar.gz -o /tmp/zookeeper-$ZK_VERSION.tar.gz

# Create required directories
RUN mkdir -p /opt && \
    mkdir -p /var/lib/zookeeper/data && \
    mkdir /var/lib/zookeeper/log

# Extract ZooKeeper, delete download
RUN tar -xz -C /opt -f /tmp/zookeeper-$ZK_VERSION.tar.gz && \
    rm /tmp/zookeeper-$ZK_VERSION.tar.gz

# Create config file
RUN echo "tickTime=2000" > /opt/zookeeper-$ZK_VERSION/conf/zoo.cfg && \
    echo "initLimit=5" >> /opt/zookeeper-$ZK_VERSION/conf/zoo.cfg && \
    echo "syncLimit=2" >> /opt/zookeeper-$ZK_VERSION/conf/zoo.cfg && \
    echo "dataDir=/var/lib/zookeeper/data" >> /opt/zookeeper-$ZK_VERSION/conf/zoo.cfg && \
    echo "dataLogDir=/var/lib/zookeeper/log" >> /opt/zookeeper-$ZK_VERSION/conf/zoo.cfg && \
    echo "clientPort=2181" >> /opt/zookeeper-$ZK_VERSION/conf/zoo.cfg && \
    echo "$MYID" > /opt/zookeeper-$ZK_VERSION/conf/myid

EXPOSE 2181 2888 3888

CMD ["/opt/zookeeper-$ZK_VERSION/bin/zkServer.sh", "start-foreground"]
