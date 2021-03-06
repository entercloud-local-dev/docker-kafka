# Entercloud engine messenger

FROM java:openjdk-8-jre

LABEL author="Andrew S Thompson Entercloud LLC andrewpsp"
LABEL maintainer="admin@entercloud.info"


ENV DEBIAN_FRONTEND noninteractive
ENV SCALA_VERSION 2.12.3 
ENV KAFKA_VERSION 0.11.0.0
ENV KAFKA_HOME /opt/kafka_"$SCALA_VERSION"-"$KAFKA_VERSION"

# Install Kafka, Zookeeper , supervisor, figlet
RUN apt-get update && \
    apt-get install -y figlet zookeeper wget supervisor dnsutils && \
    rm -rf /var/lib/apt/lists/* && \
    apt-get clean && \
    wget -q http://apache.mirrors.spacedump.net/kafka/"$KAFKA_VERSION"/kafka_"$SCALA_VERSION"-"$KAFKA_VERSION".tgz -O /tmp/kafka_"$SCALA_VERSION"-"$KAFKA_VERSION".tgz && \
    tar xfz /tmp/kafka_"$SCALA_VERSION"-"$KAFKA_VERSION".tgz -C /opt && \
    rm /tmp/kafka_"$SCALA_VERSION"-"$KAFKA_VERSION".tgz

ADD scripts/start-kafka.sh /usr/bin/start-kafka.sh

# Supervisor config
ADD supervisor/kafka.conf supervisor/zookeeper.conf /etc/supervisor/conf.d/

# 2181 is zookeeper, 9092 is kafka
EXPOSE 2181 9092

CMD ["supervisord", "-n"]
CMD ["figlet", "-c","'Entercloud Engine Messenger Interface'"]
