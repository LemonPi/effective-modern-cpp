## universal reference
- can be confused with rvalue reference
	- both are T&&
	- context dependent
		- template parameters
			- template<typename T> void f(T&& param)
		- auto declarations
			- auto&& var = var1;
		- commonality is **type deduction**
			- form must be T&&
				- std::vector<T>&& is not T&& so is an rvalue reference
				- template<typename T> void f(const T&& param) is not T&& so is const rvalue reference
			- type deduction is not guaranteed by being in a template
				- template<typename T> class vector { 
					void push_back(T&& x)
				} does not apply type deduction to the T&&
- can bind to anything
- universal references is actually a lie/abstraction
	- underlying mechanism is reference collapsing
