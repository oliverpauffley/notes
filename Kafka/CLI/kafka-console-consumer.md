# [[Kafka]]-console-consumer
You must always specify the kafka server with `--boostrap-server <bootstrap-address>` and the topic with `--topic <topic-name>`.

## Example
`kafka-console-consumer.sh --bootstrap-server 127.0.0.1:9092 --topic first_topic`

## Offset
By default the consumer will read in real time but will not go back and read from the start. Using the flag `--from-beginning` you can set to read from the first offset.

##  Groups
If you use the flag `-group <group-name>` kafka will then load balance across the consumers with the same group name. The more consumers you add kafka will automatically balance between them. Be aware the using this with the above **from-beginning** will only read from the beginning per group.
