FROM ubuntu:trusty

MAINTAINER Tom Cameron <tomc603@gmail.com>

# Environment Variables
ENV ZK_VERSION 3.4.6
ENV ZK_DIR /opt/zookeeper-$ZK_VERSION
ENV ZK_CONF_DIR $ZK_DIR/conf
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
RUN echo "tickTime=2000" > $ZK_CONF_DIR/zoo.cfg && \
    echo "initLimit=5" >> $ZK_CONF_DIR/zoo.cfg && \
    echo "syncLimit=2" >> $ZK_CONF_DIR/zoo.cfg && \
    echo "dataDir=/var/lib/zookeeper/data" >> $ZK_CONF_DIR/zoo.cfg && \
    echo "dataLogDir=/var/lib/zookeeper/log" >> $ZK_CONF_DIR/zoo.cfg && \
    echo "clientPort=2181" >> $ZK_CONF_DIR/zoo.cfg && \
    echo "$MYID" > $ZK_CONF_DIR/myid

# Create start script
RUN echo "#!/bin/sh" > /zkstart.sh && \
    echo "$ZK_DIR/bin/zkServer.sh start-foreground" >> /zkstart.sh && \
    chmod +x /zkstart.sh

EXPOSE 2181 2888 3888

CMD ["/zkstart.sh"]
