## const member thread safety
- const members should be thread safe
	- by default if it doesn't modify any mutable members then it is
	- if there are mutable members then protect with mutex or use atomic if it's simple