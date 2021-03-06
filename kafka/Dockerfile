# Kafka and Zookeeper

FROM java:openjdk-9-jre

ENV DEBIAN_FRONTEND noninteractive
ENV SCALA_VERSION 2.11
ENV KAFKA_VERSION 2.1.0
ENV KAFKA_HOME /opt/kafka_"$SCALA_VERSION"-"$KAFKA_VERSION"

# Install Kafka, Zookeeper and other needed things
RUN  apt-get update
RUN  apt-get install -y --allow-unauthenticated zookeeper wget supervisor dnsutils
RUN  rm -rf /var/lib/apt/lists/* 
RUN  apt-get clean 
RUN  wget -q http://apache.mirrors.pair.com/kafka/"$KAFKA_VERSION"/kafka_"$SCALA_VERSION"-"$KAFKA_VERSION".tgz -O /tmp/kafka_"$SCALA_VERSION"-"$KAFKA_VERSION".tgz 
RUN  tar xfz /tmp/kafka_"$SCALA_VERSION"-"$KAFKA_VERSION".tgz -C /opt 
RUN  rm /tmp/kafka_"$SCALA_VERSION"-"$KAFKA_VERSION".tgz
RUN  ln -s /usr/lib/jvm/java-9-openjdk-amd64/lib /usr/lib/jvm/java-9-openjdk-amd64/conf

ADD scripts/start-kafka.sh /usr/bin/start-kafka.sh

# Supervisor config
ADD supervisor/kafka.conf supervisor/zookeeper.conf /etc/supervisor/conf.d/

# 2181 is zookeeper, 9092 is kafka
EXPOSE 2181 9092

CMD ["supervisord", "-n"]
