# Fan-Out, Fan-In
## Fan-Out
You might consider *fanning-out* a stage in a pipeline if:
- It doesn't rely on values that the stage had calculated before.
- It takes a long time to run.

### Without Fanning out
```go
rand := func() interface{} { return rand.Intn(50000000)}

done := make(chan interface{})
defer close(done)

start := time.Now()

randIntStream := toInt(done, repeatFn(done, rand))
fmt.Println("Primes:")
for prime := range take(done, primeFinder(done, randIntStream), 10) {
	fmt.Printf("\t%d\n", prime)
}
fmt.Printf("Search took: %v", time.Since(start))
```
This is a a really slow way of finding prime numbers. It's a good candidate for fanning out as above. Normally takes about 23 seconds
### Fanning Out
```go
numFinders := runtime.NumCPU()
finders := make([]<-chan int, numFinders)
for i := 0; i< numFinders; i++ {
	finders[i] = primeFinder(done, randIntStream)
}
```

## Fan-In
```go
fanIn := func(
	done <- chan interface{}
	channels ... <- chan interface{},
) <- chan interface{} {
	var wg sync.WaitGroup
	multiplexedStream := make(chan interface{})
	
	mutlipex := func(c <- chan interface{}) {
		defer wg.Done()
		for i:= range c {
			select {
			case <- done:
				return
			case mutiplexedStream <- i:
			}
		}
	}
	
	// select from all the channels
	wg.Add(len(channels))
	for _, c := range channels {
		go mutltiplex(c)
	}
	// wait for all the reads to complete
	go func() {
		wg.Wait()
		close(multiplexedStream)
	}()
	return multiplexedStream
}
```

## All Together
```go
done := make(chan interface {})
defer close(done)

start := time.Now

rand := func() interface{} {return rand.Intn(50000000)}

randIntStream := toInt(done, repeatFn(done, rand))

numFinders := runtime.NumCPU()
fmt.Printf("Spinning up %d prime finders .\n", numFinders)
finders := make([]<- chan interface{}, numFinders)
fmt.Println("Primes:")
for i := 0; i < numFinders; i++ {
	finders[i] = primeFinder(done, randIntStream)
}

for prime := range take(done, fanIn(done, finders...), 10) {
	fmt.Printf("\t%d\n", prime)
}

fmt.Printf("Search took: %v", time.Since(start))
```
Which has the potential to reduce the time to 5 seconds.