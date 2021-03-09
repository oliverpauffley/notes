# Goroutines
Every go program has at least one goroutines: the *main goroutine*, which is automatically created and started when the process begins.
>A goroutine is a function that is running concurrently alongside other code

```go
go func() {
	fmt.PrintLn("hello")
}()
// do some other stuff
```
