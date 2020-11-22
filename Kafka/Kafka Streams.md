# [[Kafka]] Streams 
Kafka streams are a kafka to kafka process that changes the data in someway then writes back to kafka. It's the only way to get exactly once processing. Useful for dealing with concurrency and error cases.

Supported in go with [goka](https://github.com/lovoo/goka)