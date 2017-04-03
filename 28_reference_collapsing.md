## reference collapsing
- reference to reference may be produced by compilers
	- if either lvalue reference, then lvalue reference; otherwise rvalue reference
		- auto& && -> auto&
		- auto&& & -> auto&
		- auto&& && -> auto&&
		- auto && -> auto&&
		- auto&&  -> auto&&
	- occurs in 4 contexts
		1. template instantiation
		2. type generation for auto variables
		3. generation of typedefs and alias
		4. uses of decltype
- allows the abstraction of universal references
	- just reference collapsing in action combined with a specific template form