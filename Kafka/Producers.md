# [[Kafka]] Producers
Write [[Events]] to [[Brokers]] so that they can be read from by [[Consumer]]. Producer's are load balanced so that the producer automatically writes to brokers/partitions as needed. 

## Delivery Guarantees
When you commit events as a producer you can choose from 3 options for delivery guarantees.
- Async (no guarantee). `acks=0`. No accepted message is sent back. Great for logs, metrics and for speed.
- Committed to Leader. `acks=1`. Accepted message is sent back only from the leader. If the leader goes down before the brokers can be restarted you can lose data.
- Committed to Leader & Quorum. `acks=all`. A message is sent to all brokers from the leader and then back to the producer. You also need to set `min.insync.replicas`to say how many replicas as needed to exist. If the number of brokers up is less than the number of replicas set then the producer will fail to send a message. 

## Idempotent Producer
idempotent producers are used to protect from network errors. If an ack is lost from the broker and a retry is sent, the broker knows to ignore and not commit a message twice.

## Key hashing
By default keys are hashed using murmur2 algorithm. This can be changed but you don't need to. 

```java
targetPartition = Utils.abs(Utils.murmur2(record.key())) % numParitions;
```

