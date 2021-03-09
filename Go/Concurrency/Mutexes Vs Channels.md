# Mutexes Vs Channels
Go exposes low level mutexs as well as channels for methods of controlling concurrency. Although the motto goes
>Share memory by communicating, don't communicate by sharing memory

There are times when using a mutex and controlling access to a share memory resource is the right answer. The following diagrams shows the decision making process.
![[mutexvschannels.png]]

## Are you trying to transfer ownership of data?
If you have a bit of code that produces a result and wants to share that with another bit of code. Use a channel.
## Are you trying to guard internal state of a struct?
If you are trying to keep the internal state of a struct safe for concurrent usage, use a [[Sync#Mutex]].
```go
type Counter Struct {
	mu sync.Mutex
	value int
}

func (c *Counter) Increment() {
		c.mu.Lock()
		defer c.mu.Unlock()
		c.value++
}
```
