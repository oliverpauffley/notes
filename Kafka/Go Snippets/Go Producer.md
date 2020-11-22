# Go [[Producers]]
```go
func producerExample(topic string) {
	// create the producer
	w := kafka.NewWriter(kafka.WriterConfig{
		Brokers:  []string{"localhost:9092"},
		Topic:    topic,
		Balancer: &kafka.LeastBytes{},
	})

	// send data
	for i := 0; i < 10; i++ {
		w.WriteMessages(context.Background(),
			kafka.Message{
				Key:   []byte(fmt.Sprintf("id_%d", i)),
				Value: []byte(fmt.Sprintf("Hello World! %d", i)),
			},
		)
	}
	// close forces async messages to be sent.
	w.Close()
}