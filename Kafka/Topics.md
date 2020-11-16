# [[Kafka]] Topics
A topic is a particular stream of data. A bit like a table in sql.

A topic is name for 1 or more partitions. Think of it a bit like a folder that collects the [[Events]] about something. 

## Partitions
Within a topic the events are split into partitions. For a given event with a key, any event with the same key is always written to the same partition. 

You have to tell kafka how many partitions you want.

## Offsets
An offset is the ID of a given event within a partition. They are unique within a partition but not within a topic. The diagram below makes it clearer.

![[Kafka Topic.png]]

[[Kafka/Consumer]] keep track of which offset they are using together with brokers. Because of this offset consumer's can replay events. 

- Partitions are replicated across [[Brokers]] 
- Ordering is guaranteed for a partition
- They only have meaning with a partition too.


## Example
We have a topic called **trucks_gps** which contains the gps data for every truck in a trucking company.
every 20 seconds the each truck sends the following information:
- A truck ID
- Latitude
- Longitude

We arbitrarily choose to have 10 partitions (we can change later). 

## Tips
### Partition Count
Each partition can handle a throughput of a few MB/s (measure it!)
More Partitions implies:
- Better parallelism.
- Ability to run more consumers
- Ability to have move brokes.
#### Guidelines
- Partitions per topic 
	- `small cluster (<6 brokers)` 2 x num of brokers.
	- `larger clusters` 1 ish x num of brokers.
	- Remember to factor in peak demand. If you need 20 consumers for busy times you need 20 partitions.
	- test
	
### Replication Factor
should be at least 2, usually 3, max 4.
The higher the replication factor:
- better resilience of your system
- BUT more replication
- BUT more disk space needed
#### Guidelines
- Use 3.
- If this is an issue get better machines.
- **NEVER 1 IN PROD**.

### Cluster
You should not hold more 2000 to 4000 partitions on a broker. A Kafka cluster should have a maximum of 20,000 partitions across all brokers.

