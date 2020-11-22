# Zookeeper
- Manages [[Brokers]] (keeps a list of them).
- Helps to perform leader elections if one gets dropped.
- Sends notifications to kafka in case of changes (new [[Topics]], brokers etc).
- **[[Kafka]] has to have zookeeper** at the moment.
- Always has an odd number of servers (3,5,7).
- Zookeeper also has leaders and followers. 
- Zookeeper does **not** store any data on producers or consumers

