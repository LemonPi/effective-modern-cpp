## move and forward
- move unconditionally casts to rvalue
	- cannot change constness
		- const rvalue cannot be moved from, only copied
		- don't declare anything movable const (obviously)
- forward casts to rvalue if argument was initialized with an rvalue
	- remember that parameters are always lvalues even if they are rvalue references
	- mostly used when taking a universal reference parameter to pass to another function
- both do nothing at runtime
	- compile time casts

## when to use
- use std::move on rvalue references
	- don't move automatic storage locals out
		- RVO (return value optimization): compiler must copy elide or move
- use std::forward on universal references