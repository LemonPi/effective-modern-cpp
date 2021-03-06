## atomic and volatile
- often conflated ideas
- volatile is for special memory
	- normal memory assumes memory won't change unless changed by program
	- special memory means external sources can change value
		- sensors
		- displays
		- printers
		- network ports
	- prevents optimization out of redundant loads and dead stores
	- guarantees nothing for multithreading access
- atomic is for multithreaded access without mutexes
	- prevent code reordering
		- no code before a write of a std::atomic can take place after
	- execute read-modify-write operations atomically
		- ++vi;
			- if not atomic, then when executed on multiple threads could give garbage values
				- each thread must first read the value
				- if other threads read between another thread's read and write, will not update to latest value
					- thread 1 loads vi -> 0
					- thread 2 loads vi -> 0
					- thread 1 increments value -> 1
					- thread 2 increments value -> 1
					- thread 2 stores vi <- 1
					- thread 1 stores vi <- 1