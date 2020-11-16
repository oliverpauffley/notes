# [[Kafka]] Events/Records
An event records that something has happened in the world or in the business. Every event has the following fields

- Event **Key**: "Alice"
- Event **Value**: "Made a payment of $200 to Bob"
- Event **Timestamp**: "Jun. 25, 2020 at 2:06pm"
and optional metadata headers.

Events are **Immutable** and append only.
Events are persisted to disk.

[[Producers]] create or publish new events.
[[Consumer]] subscribe to these events.
Events are stored in [[Topics]] 
[[Brokers]] are nodes that store events. 

## Keys
[[Producers]] can choose to send a **key** with the message (string, int , etc...)
If key = null, data is sent round robin (broker 1, broker 2, broker 3 ...)
If a key is send, then all messages for that key will go to the same partition.  
A key should be specified if you need the messaged to be **ordered**.  