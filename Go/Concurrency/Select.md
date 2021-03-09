# Select
```go
var c1, c2 <- chan interface{}
var c3 chan <- interface{}

select {
case <- c1:
	// Do something
case <- c2:
	// Do something
case c3 <- struct{}{}:
	// Do something
}
```
`select` blocks look a lot like [[switch]] blocks. They have some similarities but they have some key differences.
- blocks are tested sequentially
- execution won't fall through if no criteria are met.
Instead all channel reads and writes are considered simultaneously to see if any are ready. populated or closed channels for reads and non-full channels in the case of writes.

If no statements are ready then the `select` statement will block. Then as soon as one channel is ready the operation will proceed.

If multiple statements are ready at the same time the go runtime will load balance across the statements pseudo-randomly.

If no statements are every ready then you will be blocked forever. You could do something like so to *timeout*.
```go
var c <- chan int
select {
case <- c:
case <- time.After(1 * time.Second):
	fmt.Println("Timed out.")
}
```
This will always timeout in this case as we are reading from a `nil` channel.

## Default 
Just like a [[switch]] statement a select can have a default case. This will be called if none of the other cases are ready. A classic use case to run a for loop until something is finished.
```go
done := make (chan interface{})
go func {
	time.Sleep(5* time.Second)
	close(done)
}()

workCounter := 0
loop:
for {
	select {
		case <- done:
		break loop
	default:
	}
	// simulate work
	workCounter ++
	time.Sleep(1*time.Second)
}

fmt.Printf("Achieved %v cycles of work before signalled to stop. \n", workCounter)
```
This will achieve 5 cycles of work whilst checking between each cycle to see if it should stop.

## Empty select
```go
select {}
```
Will just block forever.