# [[Kafka]] Consumer
Consumers read and process [[Events]].

## Consumer groups
by creating consumer groups. You can distribute load across multiple services. For example. If you have two [[Pods]] that are running a particular service, the consumer groups with make sure that each event is only read by one consumer within the group.

This load balancing is handled by kafka.

![[Consumer Groups.png]]

## Read Guarantees
When reading messages as a group there are a number of options.
- At least once.
- At most once.
- Effectively once. 
- Exactly once (maybe but not realistic).