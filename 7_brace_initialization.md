## brace initialization
- 4 initializer methods
	- int x(0);
	- int y = 0;
	- int z{0};
	- int z = {0};
		- treated the same as int z{0};
- uncopyable objects cannot be initialized with "="
- brace initialization checks for implicit narrowing conversions
- {} means empty arguments rather than empty initializer list
	- avoids most vexing parse
		- Widget w2(); is a function returning Widget rather than a default constructed Widget
- for classes with ctor defined taking in initializer list, it is strongly preferred
	- very hard to call any overloading ctor even if they are a better fit
	- generally avoid creating classes taking initializer list unless the overloaded ctor parameter types are sufficiently different
	- problem with std::vector<numeric_type> with 2 arguments
		- std::vector<int> v(10, 20); creates 10 elements all with value 20
		- std::vector<int> v{10, 20}; creates 2 elements 10 and 20
	- similar problem with std::make_unique and std::make_shared
		- they use parenthesis in the constructor