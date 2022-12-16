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