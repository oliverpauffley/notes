# Brokers
A kafka cluster is compose of multiple brokers (servers) similar to [[Kubernetes]] clusters and nodes.

Each broker contains only certain [[Topics]] partitions. They are split across the brokers in your cluster.

If you have 3 brokers and two different topics they would be split as follows:
![[brokers_topics.png]]

## Topic replication
You can define a replication factor. These tells kafka to replicate the topic partitions in such a way that the number of copies you request exist on your brokers. 

One broken is assigned as the **leader**. This leader is in charge of sending and receiving data for this partition. Other brokers become passive storage in-case of failures.

![[replication_factor.png]]

## Broker Discovery
Every kafka broker is also called a `bootstrap server`
That means that you **only need to connect to one broker**, and you will be connected to the whole cluster. 
Each broker knows about all brokers, topics and partitions (stored as metadata).

![[broker_discovery.png]]

