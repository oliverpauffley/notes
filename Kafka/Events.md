# [[Kafka]] Events/Records
An event records that something has happened in the world or in the business. Every event has the following fields

- Event **Key**: "Alice"
- Event **Value**: "Made a payment of $200 to Bob"
- Event **Timestamp**: "Jun. 25, 2020 at 2:06pm"
and optional metadata headers.

Events are **Immutable** and append only.
Events are persisted to disk.

[[Producers]] create or publish new events.
[[Consumers]] subscribe to these events.
Events are stored in [[Topics]] 
[[Brokers]] are nodes that store events. 
