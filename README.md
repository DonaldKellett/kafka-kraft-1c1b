# kafka-kraft-1c1b

Apache Kafka Raft \(KRaft\) cluster with 1 controller, 1 broker using Docker Compose

## Getting started

You should have Docker Engine and Docker Compose V2 installed.

Start the Kafka cluster:

```bash
docker compose up -d
```

Interact with the Kafka cluster. Invoke `kafka-topics.sh` in the controller as below to create a new topic `kafka-hello-world`:

```bash
docker exec kafka-controller-0 \
    /opt/bitnami/kafka/bin/kafka-topics.sh \
    --bootstrap-server kafka-broker-0:9092 \
    --create \
    --topic kafka-hello-world
```

Next, open a new terminal window and start the Kafka console consumer with `kafka-console-consumer.sh`:

```bash
docker exec -it kafka-controller-0 \
    /opt/bitnami/kafka/bin/kafka-console-consumer.sh \
    --bootstrap-server kafka-broker-0:9092 \
    --topic kafka-hello-world \
    --from-beginning
```

Now return to the original terminal window and start the Kafka console producer with `kafka-console-producer.sh`:

```bash
docker exec -it kafka-controller-0 \
    /opt/bitnami/kafka/bin/kafka-console-producer.sh \
    --bootstrap-server kafka-broker-0:9092 \
    --topic kafka-hello-world
```

Enter a few messages separated by newlines using the console producer and observe the messages appearing in the console consumer window.

Stop the Kafka cluster:

```bash
docker compose down
```

## License

[Apache 2.0](./LICENSE)
