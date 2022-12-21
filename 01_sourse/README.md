## Kafka Cluster (standalone) Connect

```bash
    docker-compose up kafka-cluster
```
- Go inside container, and mount files
```bash
    docker run --rm -it -v "$(pwd)":/tutorial --net=host landoop/fast-data-dev:latest bash
```
- Create topic
```bash
  kafka-topics --create --bootstrap-server 127.0.0.1:9092 --topic demo-1-standalone --partitions 3 --replication-factor 1 
```
- CD to 01_source inside container and type
```bash
  cd tutorial/01_source
  connect-standalone worker.properties file-stream-demo-standalone.properties 
```

## Pure Kafka
- Go inside kafka
- Start Zookeeper
- Start Broker
```bash
  bin/zookeeper-server-start.sh config/zookeeper.properties
  
  bin/kafka-server-start.sh config/server.properties
```
- Create file `test.txt` and add data there
- Change configuration
```bash
  cat config/connect-standalone.properties 
```
```bash
  plugin.path=libs/connect-file-3.3.1.jar
```
- Create topic
```bash
  cat config/connect-file-source.properties 
```
```bash
  ...
  topic=connect-test
```
```bash
  bin/kafka-topics.sh --bootstrap-server localhost:9092 --create --topic connect-test
```
- Create consumer
```bash
  bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic connect-test --from-beginning
```
- Start processing
```bash
  bin/connect-standalone.sh config/connect-standalone.properties config/connect-file-source.properties
```
- Add data to file
```bash
  nano test.txt 
```
