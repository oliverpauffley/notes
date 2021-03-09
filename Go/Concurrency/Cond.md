# Cond
from the type description for `Cond`.
>... a rendezvous point for goroutines waiting for or announcing the occurrence of an event.

It is used to run infinite loops until some condition happens. It is must more efficient than just using a loop however.
```go
c := sync.NewCond(&sync.Mutex())
c.L.Lock()
for conditionTrue() == false {
	c.Wait()
}
c.L.Unlock()
```
This is much more efficient than just 
```go
for conditionTrue() == false {
}
```

A more complete example. If we have a queue of fixed length 2, and 10 items we want to push onto the queue. We want to enqueue items as soon as there is room. so we want to be notified as soon as there's room in the queue.
```go
c := sync.NewCond(&sync.Mutex{})
queue := make([]interface{}, 0, 10)

removeFromQueue := func(delay time.Duration) {
	time.Sleep(delay)
	c.L.Lock()
	queue = queue[1:]
	fmt.Println("Removed from queue")
	c.L.Unlock()
	s.Signal()
}

for i := 0; i < 10; i++ {
	c.L.Lock()
	for len(queue) == 2 {
		c.Wait()
	}
	fmt.Println("Adding to queue")
	queue = append(queue, struct{}{})
	go removeFromQueue(1 *time.Second)
	c.L.Unlock()
}
```
Cond's is also super useful as it has a method called `Broadcast()` that can be used to communicate with multiple goroutines at the same time. For example a button click could signal a Cond `Broadcast` then makes multiple things fire off.