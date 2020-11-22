# [[Kafka]] Schema Registry

It's very important that the data format is agreed upon. This can be any format but normal ones are json, gRPC or avro. You can run a schema registry that will check the format of producer messages before they reach kafka. 