# [[Kafka]] Consumer
Consumers read and process [[Events]].

Consumers read from [[Brokers]] and each partition is read in order. Consumers can read from multiple partitions but there is no ordering between partition. 

## Consumer groups
by creating consumer groups. You can distribute load across multiple services. For example. If you have two [[Pods]] that are running a particular service, the consumer groups with make sure that each event is only read by one consumer within the group.

This load balancing is handled by kafka. If there are more consumer groups than partitions, some will be inactive. The number of partitions needs to be higher than number of consumers to maximize throughput.

![[Consumer Groups.png]]

## Read Guarantees
When reading messages as a group there are a number of options.
- At least once. Offsets are committed after the messages are received. Messages are replayed if the server goes down. Sometimes messages will be done twice. Important to make the processing **idempotent**.
- At most once. Offsets are committed as soon as they are received. Messages are lost if they are not processed correctly.
- Effectively once. 
- Exactly once (maybe but not realistic). Only with kafka streams.

## Consumer Polls
Kafka consumers "poll" for messages rather than being "pushed" them. This means that consumer control when they receive messages, where they start consuming from and means they can replay events. These can be changed by changing the `min.bytes` `max.poll.records` `max.parition.fetch.bytes` `fetch.max.bytes` mostly don't need to be changed.

## Commit Strategies [needs samara not kafka-go]
Two common patterns
- enable.auto.commit = true & synchronous processing of batches
- enable.auto.commit = false & manually commit offsets.
### Auto commit
This means that kafka handles the committing for you. This means that no matter what happens after the message is received the offset is already committed. 
### Manual commit
This means that you can only commit when something is successfully processed.

## Replaying events
use the [[kafka-consumer-groups#Reset Offsets]] to reset the offsets for a given consumer group. Ensure the consumer is idempotent.

## Hearbeat Thread
Each consumer sends a "heartbeat" message to one broker. The cutoff point to determine if a consumer is down and how frequently the consumer will send a message to the heartbeat broker can be changed.

## Poll Thread
The setting `max.poll.interval.ms` is the maximum amount of time between poll calls before a consumer is declared as dead. If data takes longer than 5 mins to process this might be worth increasing.