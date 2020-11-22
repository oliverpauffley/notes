# Kafka Guarantees
on top of information on [[Producers#Delivery Guarantees]] and [[Kafka/Consumer#Read Guarantees]] some important facts:
- Message are appended in the order they are sent.
- Consumers read messages in the order they have been stored in partitions.
- With a replication factor of N, producers and consumers can tolerate up to N-1 brokers being down.
- As long as the number of partitions remains constant, the same key will go to the same partition.