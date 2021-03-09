# GOMAXPROCS
Prior to go 1.5 you had to set `GOMAXPROCS` to tell go how many OS threads that will host work queues. However it is now automatically set! [[Goroutines]] will automatically use all the threads available.

