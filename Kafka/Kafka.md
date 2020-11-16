# Kafka
Kafka is a messaging system designed to handle events in a hugely scaleable way. Really an event ledger. **A Distributed Commit Log**.

Kafka will ensure events are ordered.

![[concept_diagram.png]]

## [[Events]]
## [[Producers]]
## [[Consumer]]
## [[Topics]]
## [[Brokers]]
## [[Zookeeper]]

![[Kafka Simple Example.png]]

Figure: This example topic has four partitions P1–P4. Two different producer clients are publishing, independently from each other, new events to the topic by writing events over the network to the topic's partitions. Events with the same key (denoted by their color in the figure) are written to the same partition. Note that both producers can write to the same partition if appropriate.