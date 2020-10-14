# [[Kafka]] Producers
Write [[Events]] to [[Brokers]] so that they can be read from by [[Consumers]]

## Delivery Guarantees
When you commit events as a producer you can choose from 3 options for delivery guarantees.
- Async (no guarantee).
- Committed to Leader.
- Committed to Leader & Quorum.