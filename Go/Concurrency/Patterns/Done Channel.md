# Done Channel
> If a goroutine is responsible for creating a goroutine, it is also responsible for ensuring it can stop the goroutine.

Leaving a channel open forever is not free and in the worst case can balloon and crash a program.

```go
newRandStream := func(done <- chan interface{}) <- chan int {
	randStream := make(chan int)
	go func() {
		defer fmt.Println("newRandStream closure exited.")
		defer close(randStream)
		for {
			select {
				case randStream <- rand.Int():
				case <- done:
					return
			}
		}
	}
	return randStream
}

close (done)
```
Here by closing the done channel there is a way of breaking the other channel being written to.