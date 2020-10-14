# [[Kafka]] Topics
A topic is name for 1 or more partitions. Think of it a bit like a folder that collects the [[Events]] about something. 

## Partitions
Within a topic the events are split into partitions. For a given event with a key, any event with the same key is always written to the same partition. 

## Offsets
An offset is the ID of a given event within a partition. They are unique within a partition but not within a topic. The diagram below makes it clearer.

![[Kafka Topic.png]]

[[Consumer]] keep track of which offset they are using together with brokers. Because of this offset consumer's can replay events. 

- Partitions are replicated across [[Brokers]] 
- Ordering is guaranteed for a partition