# [[Kafka]]-console-producer
you must always specify the broker with `--broker-list <broker-address>` and the topic with `--topic <topic-name>`.

## Connect
`kafka-console-producer.sh --broker-list 127.0.0.1:9092 --topic first_topic`
note that this works even if the topic has not already been defined! **probably not a good idea** as the topic has default setups.

## With different properties
`kafka-console-producer.sh --broker-list 127.0.0.1:9092 --topic first_topic --producer-propery acks=all`