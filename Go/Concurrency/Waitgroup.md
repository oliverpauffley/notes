# Waitgroup
Waitgroups are useful when you don't care about the result of a set of operations or you have other means of collecting results. If neither of those are true a [[Select]] is a better choice.
```go
var wg sync.WaitGroup

wg.Add(1)
go func() {
	defer wg.Done()
	fmt.PrintLn("1st goroutine sleeping...")
	time.Sleep(1)
}

wg.Add(1)
go func() {
	defer wg.Done()
	fmt.PrintLn("2nd goroutine sleeping...")
	time.Sleep(1)
}

wg.Wait()
fmt.PrintLn("all goroutines complete.")
```
You have to call `wg.Add(1)` outside of the goroutine otherwise you can't guarantee that the `wg.Add` would be called before the `wg.Wait()`

Normally you want to put the `wg.Add` as close as you can to the goroutine. However with a loop you might do one `wg.add`  for the whole loop
```go
hello := func(wg *sync.WaitGroup, id int) {
	defer wg.Done()
	fmt.Printf("Hello from %v\n", id)
}

const numGreeters = 5
var wg sync.WaitGroup
wg.Add(numGreeters)
for i := 0; i< numGreeters; i++ {
	go hello(wg, i)
}

wg.Wait()
```
