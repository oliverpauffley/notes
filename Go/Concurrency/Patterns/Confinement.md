# Confinement
> Confinement is the idea that information is only ever available from **one** concurrent process.
When this is achieved a concurrent program is implicitly safe and no synchronization (with things like mutexes) is needed.

## Ad-hoc
Ad-hoc confinement is when you achieve confinement through a convention. It's hard to do as everyone who commits code might break the convention.
```go
data := make([]int, 4)

loopData := func(handleData chan<- int) {
	defer close(handleData)
	for i := range data {
		handleData <- data[i]
	}
}

handleData := make(chan int)
go loopData(handleData)

for num := range handleData {
	fmt.Println(num)
}
```
`data` is available from both the `loopData` function and `handleData` channel. By convention we only access `data` in the `loopData` function. But this can be missed or changed and it's hard to spot.

## Lexical
Lexical confinement involves using lexical scope to expose only the correct data and concurrency primitives for multiple concurrent processes to use. **It makes it impossible to do the wrong thing**.