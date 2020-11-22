# Consumer Offsets
Kafka stores the offsets at which a [[Kafka/Consumer]] group has been reading. The offsets are actually committed live in a kafka topic called `__consumer_offsets`.
If a consumer dies, it can read the consumer offset to know where to reset from.

This can be setup to get the behaviors described in [[Kafka/Consumer#Read Guarantees]]. 