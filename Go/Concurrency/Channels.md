# Channels
Channels are best used to communicate information between [[Goroutines]]. They can be combined together with the [[Select]] statement. 

>Like a river, a channel serves a conduit for a stream of information; values may be passed along the channel, and then read out downstream.

For this reason ending a `chan` variable name with "Stream" is nice. Make a new channel with `dataStream = make(chan interface{})`

You can also create channels that can only be read or written from. 
- Only read:
```go
var dataStream <- chan interface{}
// or
dataStream := make(<- chan interface{})
```
- Only Write
```go
var dataStream  chan <- interface{}
// or
dataStream := make( chan <- interface{})
```
Mostly this is useful for function parameters and return types as go will automatically convert channels into unidirectional as needed and this limits there use within a function.

## Sending and Receiving 
- Sending is done with `<-` on the right hand side of the channel.
- Receiving is done with `<-` on the left hand side of the channel.
```go
stringStream := make(chan string)
go func() {
	stringStream <- "hello Channels!!!"
}()
fmt.Println(<-stringStream)
```
This is thread safe as the call to print will block until a value is sent onto the channel. The program would deadlock if a value is never sent to the channel.

### Reading from closed channels
You can optional read two values from a channel like so:
```go
salutation, ok := stringStream
```
Which will return `Hello Channels!!!`, `ok` The boolean indicates that the read was a value from the channel rather than one generated from a closed channel. 
Closing a channel signifies that we are finished writing values to a channel. You can read from closed channels.
```go
intStream := make(chan int)
close(intStream)
integer, ok := <- intStream
fmt.Printf("(%v): %v", ok, integer)
```
will produce `(false): 0`. So even though we never write to the channel we can still read from it. A zero value for the `int` type is returned and a false to show the channel is closed. This means that we can range over the values in a channel and go will handle the final returned value.

### Ranging over channels
```go
intStream := make(chan int)
go func() {
	defer close(intStream)
	for i := 1; i <= 5; i++ {
		intStream <- i
	}
}()

for integer := range intStream {
	fmt.Printf("%v", integer)
}
```
This is a very common pattern and handles the closed channel automatically in the `range` over channel.

### Closed channel as a signal
Closing a channel is also a way to signal multiple goroutines at the same time. If you have `n` goroutines reading from one channel, you can just close the channel to unblock all the goroutines.
```go
begin := make(chan interface{})
var wg sync.WaitGroup
for i := 0; i < 5 ; i++ {
	wg.Add(1)
	go func(i int) {
		defer wg.Done()
		<- begin
		fmt.Print("%v has begun\n", i)
	}(i)
}

fmt.Println("Unblocking goroutines...")
close(begin)
wg.Wait()
```
here the goroutines will be blocked reading `<-begin` until the channel is closed. So will return
```
Unblocking goroutines...
4 has begun
2 has begun
3 has begun
0 has begun
1 has begun
```

### Buffered Channels
Buffered channels are channels with a certain *capacity*. This means that event if no reads are performed you can still write to that channel `n`times, where `n` is the capacity of the channel.
```go
dataStream = make(chan interface{}, 4)
```
Buffered channels are often a premature optimization that end up hiding deadlocks.
#### When to use
If a goroutine making writes to a channel has knowledge of how many writes it will make, it can be useful to create a buffered channel whose capacity is the number of writes to be made.