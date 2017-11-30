# Apache Kafka Consumer Application

## Table of Contents

  * [Run Zookeeper](#run-zookeeper)
  * [Run three instances of Broker](#run-three-instances-of-broker)
  * [Create Topic with three partitions and three replicas](#create-topic-with-three-partitions-and-three-replicas)
  * [Run Consumer ](#run-consumer)
  * [Produce bulk messages](#produce-bulk-messages)
  * [Helpful Commands](#helpful-commands)
    * [Command to add partition](#command-to-add-partition)
    * [Command to see topics created](#command-to-see-topics-created)
  * [Prequisites](#prequisites)


## Run `Zookeeper`
```sh
$ cd kafka_2.12-1.0.0

$ .\bin\windows\zookeeper-server-start.bat config\zookeeper.properties

```

## Run three instances of `Broker`

Copy `server.properties` from `config` directory and make three copies of it and rename to `server2.properties` and `server3.properties` 

```sh
$ cd kafka_2.12-1.0.0

$ .\bin\windows\kafka-server-start.bat config\server.properties

$ .\bin\windows\kafka-server-start.bat config\server2.properties

$ .\bin\windows\kafka-server-start.bat config\server3.properties

```

## Create `Topic` with three partitions and three replicas
```sh
$ cd kafka_2.12-1.0.0

$ .\bin\windows\kafka-topics.bat --create --topic my-topic --zookeeper localhost:2181 --replication-factor 3 --partitions 3

$ .\bin\windows\kafka-topics.bat --create --topic my-other-topic --zookeeper localhost:2181 --replication-factor 1 --partitions 3

```

## Run Consumer 
```sh
$ mvn clean install
$ mvn exec:java -Psubscribe
$ mvn exec:java -Passign
```

## Produce bulk messages
```sh
$ cd kafka_2.12-1.0.0
$ .\bin\windows\kafka-producer-perf-test.bat --topic my-other-topic --num-records 50 --record-size 1 --throughtput 10 --producer-props bootstrap.servers=localhost:9092 key.serializer=org.apache.kafka.common.serialization.StringSerializer value.serializer=org.apache.kafka.common.serialization.StringSerializer
```

## Helpful Commands
### Command to add partition
```sh
$ cd kafka_2.12-1.0.0
$ .\bin\windows\kafka-topics.bat  --zookeeper localhost:2181 --alter --topic my-topic --partitions 4
```
### Command to see topics created
```sh
$ cd kafka_2.12-1.0.0
$ .\bin\windows\kafka-topics.bat --zookeeper localhost:2181 --describe
```


## Prequisites
- Kafka 2.12-1.0.0
- Scala 2.12.4
- Jdk 1.8
- Maven 3.x
