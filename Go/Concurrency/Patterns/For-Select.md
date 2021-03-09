# The For-Select Loop
```go
for { // Either loop infinitely or range over something
	select {
		// Do some work with channels
	}
}
```
## Sending iteration into a channel
```go
for _, s := range [] string {"a", "b", "c"}{
	select {
		case <- done:
			return
		case stringStream <- s:
	}
}
```
## Looping until stopped
```go
for {
	select {
		case <- done:
			return
		default :
	}
	
	// Do some non-preemptable work
}
```
