# [[Kafka]]-topics
you normally need to reference where zookeeper is with `--zookeeper <zookeeper_address>`

## Create
`kakfa-topics.sh --zookeeper 127.0.0.1:2181 --topic <topic_name> --create --partitions 3 --replication-factor 1`

## List 
`kaka-topics.sh --zookeeper 127.0.0.1:2181 --list`

## Describe
`kafka-topics.sh --zookeeper 127.0.0.1:2181 --topic <topic_name> --describe`

## Delete
``
`kafka-topics.sh --zookeeper 127.0.0.1:2181 --topic <topic_name> --delete`