# Once
```go
var count int

increment := func() {
	count++
}

var once sync.Once

var increments sync.WaitGroup
increments.Add(100)
for i := 0; i < 100; i++ {
	go func() {
		defer increments.Done()
		once.Do(increment)
	}
}

increments.Wait()
fmt.Printf("count is %d\n", count)
```
It looks like the count with be 100. But since the call to increment is wrapped in `once.Do`the call can only ever happen once. Note that each `sync.Once` counts any call to `once.Do`even with different functions.